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
   **Traditional property definition**::

      property = key: value

   **ConfigHub property definition**::

      property = key: [  value + context_1,
                         value + context_2,
                         ... ]

When an application/client requests configuration, they only need to specify their context.  Using a request
context, the exact key-value pairing occurs, and the result is returned to the client.

Using example above, a request context ``Production`` would return::

   http.port: 80
   http.redirect: 443

While a request with context ``Development`` would return::

   http.port: 8080
   http.redirect: 8443


