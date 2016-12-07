.. _primer:

ConfigHub Primer
^^^^^^^^^^^^^^^^

All configuration can be boiled down to key-value pairs (properties).  Ignoring the format
that surrounds various configuration components, configuration differences can be reduced to properties.

For example, in **Development** environment, a config file may contain a line like:
.. code-block::

    <Connector port="8080" redirectPort="8443"/>

While in **Production** the same line looks like this:
.. code-block::

    <Connector port="80" redirectPort="443"/>

Therefore, the merged configuration could be written as:

.. code-block::

    <Connector port="${ http.port }" redirectPort="${ http.redirect }"/>

And we have our two properties:  ``http.port`` and ``http.redirect``.
