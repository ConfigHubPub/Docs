.. _security:

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
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the security group is created, you can add any number of properties and files to it.
To assign an existing property to a security group, you need to add a security group to the key.

When you assign a file or a property key to a security group, their content is protected by the security group.  This
means, to edit key/value/file a security group password has to be entered.  If a security group is defined to encrypt
data, UI will not display the value and the API Pull requests will return the encrypted content for the value/file,
unless pre-authorized token or security group password is supplied in the API request.


Assignment to a property
------------------------

.. image:: /images/keySecurityGroup.png



Assignment to a file
--------------------

.. image:: /images/fileSecurityGroup.png



Tokens
^^^^^^

Tokens are for client API requests.  They identify a repository, and may pre-authorize decryption of properties and files
assigned to security groups.

.. image:: /images/token.png