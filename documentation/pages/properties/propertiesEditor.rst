.. _propertiesEditor:

Properties editor
^^^^^^^^^^^^^^^^^

Properties editor is the default view of ConfigHub UI where all/resolved properties are managed.
The properties toolbar allows provides following functionality:

.. image:: /images/propertiesToolbar.png


1. **Context selection**
    These fields allow you to set the working context, and view configuration that is "resolved" by that context.
    Unlike the context requested by the client, editor context can have multiple context elements specified in
    a single context hierarchy.

    For example, if you wanted to see configuration returned for both *Production* and *Development* environments,
    you could select both in the Environment context hierarchy.  The returned configuration would show all
    keys and values that can be returned for the combination of the specified context.

    We call this type of context - where any number of context elements can be selected per context hierarchy, a
    **non-qualified context**;


2. **Search type**

3. **New property**

4. **Comparison View**

5. **All key toggle**

6. **Key sort order**

7. **Value context alignment**

8. **Pagination navigation**