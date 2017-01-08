.. _properties:

**********
Properties
**********

Properties are traditionally defined as:::

    key: value

In ConfigHub, a property is defined with a context attached to the value.  This schema allows
many values to be assigned to a single key, with the requirement that each value's context
is unique among other values assigned to the same key.::

    key: [
        context: value,
        context: value,
        ...
    ]

Following sections show how context properties and context elements are created, edited and deleted.


.. toctree::
    :titlesonly:

    properties/propertiesEditor
    properties/createProperty
    properties/editDeleteProperty
    properties/manageContextElement
