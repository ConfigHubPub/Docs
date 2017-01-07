.. _properties:

**************************
Managing Config Properties
**************************

Properties are traditionally defined as:::

    key: value

In ConfigHub, a property is defined with a context attached to the value part.  This allows
multiple values to be assigned to a single key, with the requirement that each value's context
is unique among other values assigned to the same key.::

    key: [
        context: value,
        context: value,
        ...
    ]

.. toctree::
    :titlesonly:

    properties/createProperty
    properties/editDeleteProperty
    properties/manageContextElement
