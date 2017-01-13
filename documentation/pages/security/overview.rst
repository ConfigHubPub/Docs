.. _security:

********
Overview
********


All API transactions between the client and the ConfigHub service are made using HTTPs secure protocol.  Private
installation can be configured to also use HTTP (non-secure) protocol, but then risk in-flight security breach.

Security groups
^^^^^^^^^^^^^^^

Security Group is an abstract wrapper to which properties and/or files may be assigned.  Security Group is
password protected, so any modification of the data contained in them requires authentication before the change is
allowed.

In addition to a password challenge, security group may also be defined with **Encryption** enabled using one of
several provided cyphers.  If enabled, content assigned to a security group will, in addition to being password
protected, be encrypted, using the selected cypher and the security group's password.

.. image:: /images/securityGroup.png

Securing files and properties
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once the security group is created, you can add any number of properties and files to it.

To assign an existing property to a security group, you need to add a security group to the key.


Assignment to a property
************************
.. image:: /images/keySecurityGroup.png



Assignment to a file
************************
.. image:: /images/fileSecurityGroup.png

