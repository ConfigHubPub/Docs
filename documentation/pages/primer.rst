.. _primer:

ConfigHub Primer
^^^^^^^^^^^^^^^^

All configuration can be boiled down to key-value pairs (properties).  Ignoring the format
that surrounds various configuration components, configuration differences are always reduced to properties.

For example, in **Development** environment, a config file may contain a line like::

    <Connector port="8080" redirectPort="8443"/>

While in **Production** the same line looks like this::

    <Connector port="80" redirectPort="443"/>

Therefore, the merged configuration could be written as::

    <Connector port="${ http.port }" redirectPort="${ http.redirect }"/>

And we have our two properties:  ``http.port`` and ``http.redirect``.


Context Properties
~~~~~~~~~~~~~~~~~~

In order to eliminate a mesh of configuration file and property duplication, ConfigHub changes the definition
of a property.  By assigning a context to a property value, a single property key can have multiple values,
each with a unique context signature.

.. note::

   ConfigHub property definition:

   | property = key: [ value + context_1,
   |                   value + context_2,
   |                   ...
   |                 ]

When an application/client requests configuration, they only need to specify their context.  Using a request
context, the exact key-value pairing occurs, and the result is returned to the client.

Using example above, a request context ``Production`` would return::

   http.port: 80
   http.redirect: 443

While a request with context ``Development`` would return::

   http.port: 8080
   http.redirect: 8443

In this example, context is very simple - its composed with a single context hierarchy, Environment.  However,
context can be as complex as your environment demands - up to 10 context element hierarchy.


Context Resolution
~~~~~~~~~~~~~~~~~~

Context resolution is a process during which value-context of each key is compared to the request context in order
to determine which properties should be returned.

Matching value to request context occurs in two steps:

1. Semantic Filter
------------------

   In this, first step, for each context block, corresponding context item from value and request are compared.
   For a match, corresponding context items have to satisfy following rules:

   * If both are specified, they have to be the same;
   * Either or both are a wildcard.

   .. role:: nb
   .. role:: sr
   .. role:: gt


   **Example**: Context-Request resolution

   +---------------------+------------------+---------------+---------------+-----------------+
   |                     | Environment      | Application   | Instance      |                 |
   +=====================+==================+===============+===============+=================+
   | Request-Context     | Production       | WebServer     | Webserver-Jim |                 |
   +---------------------+------------------+---------------+---------------+-----------------+

   +---------------------+------------------+---------------+---------------+-----------------+
   | Value-Context       | Production       | WebServer     | :nb:`\*`      | :sr:`Match`     |
   +---------------------+------------------+---------------+---------------+-----------------+
   | Value-Context       | Production       | :nb:`\*`      | :nb:`\*`      | :sr:`Match`     |
   +---------------------+------------------+---------------+---------------+-----------------+
   | Value-Context       | :nb:`\*`         | :nb:`\*`      | Webserver-Jim | :sr:`Match`     |
   +---------------------+------------------+---------------+---------------+-----------------+
   | Value-Context       | :gt:`Development`| :nb:`\*`      | :nb:`\*`      | :gt:`No Match`  |
   +---------------------+------------------+---------------+---------------+-----------------+


   .. image:: /images/semanticFilter.png


2. Weight Filter
----------------

   Weighted filter is only applied in case where request context specified is a fully-specified context.

   As repository's context scope can vary in size (see Choosing Repository Context Scope), each of the context
   blocks is assigned specific weight. The widest scope specifications (left) carry less weight, while most
   specific parts (right) carry most weight.
