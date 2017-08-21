.. _install:

Installation
^^^^^^^^^^^^


.. _system-requirements:

System requirements
~~~~~~~~~~~~~~~~~~~

The ConfigHub server application has the following prerequisites:

* Some modern Linux distribution (Debian Linux, Ubuntu Linux, or CentOS recommended)
* MySQL 5 or PostgreSQL 9 or later (latest stable version is recommended)
* Oracle Java SE 8 or later (latest stable update is recommended)


Download and install
~~~~~~~~~~~~~~~~~~~~

* Download and install Java8 to your localhost.  Set the ``JAVA_HOME`` environment variable to Java's bin directory::

   export JAVA_HOME=/path/to/java8/bin

* `Download <https://www.confighub.com/download>`_ the latest version of ConfigHub:

* Uncompress the downloaded file::

   tar -xzvf confighub-<version>.tar.gz


ConfigHub service configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are two configuration sections:
   1. Database connections
   2. Server configuration

* Database connections

Database connections are configured in ``confighub-<version>/server/conf/tomee.xml`` file.
ConfigHub uses 2 databases, one for storage of all repository and user related data, and the other
for the storage of all client API requests.

As of version v1.6, ConfigHub supports MySQL and PostgreSQL databases.  Here's an example of
a database configuration:

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <tomee>

       <Resource id="ConfigHubMainDS" type="DataSource">
           JdbcDriver = org.postgresql.Driver
           JdbcUrl = jdbc:postgresql://127.0.0.1:5432/ConfigHubMain
           UserName = username
           Password = password

           validationQuery="SELECT 1"
           JtaManaged = false
           initialSize = 20
           maxActive = 100
           maxIdle = 50
           maxWaitTime = 3 seconds
           minEvictableIdleTime = 3 seconds
           numTestsPerEvictionRun = 30
       </Resource>

       <Resource id="ConfigHubApiRequestsDS" type="DataSource">
           JdbcDriver = com.mysql.jdbc.Driver
           JdbcUrl = jdbc:mysql://127.0.0.1:3306/ConfigHubClientRequests
           UserName = username
           Password = password

           validationQuery="SELECT 1"
           JtaManaged = false
           initialSize = 20
           maxActive = 50
           maxIdle = 50
           maxWaitTime = 3 seconds
           minEvictableIdleTime = 3 seconds
           numTestsPerEvictionRun = 30
       </Resource>

   </tomee>

The resource IDs ``ConfigHubMainDS`` and ``ConfigHubApiRequestsDS`` as well as parameter
``JtaManaged = false`` have to remain unchanged.  The rest of the datasource definition can
be modified to your specific needs.

.. note::  For the rest of the the optional parameters, please consult `Tomee documentation <http://tomee.apache.org/datasource-config.html>`_


* Server configuration

Edit the configuration file ``confighub.properties`` in confighub-<version> directory.
Each configuration parameter has to be specified.

.. code-block:: bash

   # Path to the location where all ConfigHub service logs are stored.
   confighub.logging.path = /var/log/confighub

   # Memory assigned to the ConfigHub service.  It is recommended to assign 4g or more.
   confighub.memory = 4g

   # HTTP and HTTPs ports
   confighub.http.port = 80
   confighub.https.port = 443

   # Specify an override to the default self-signed certificate/keystore.
   confighub.https.keystoreFile = cert/confighub_default.jks
   confighub.https.keystoreAlias = confighub
   confighub.https.keystorePass = confighub





Starting and stopping ConfigHub service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Start ConfigHub::

   confighub-<version>/server/bin/startup.sh

* Stop ConfigHub::

   confighub-<version>/server/bin/shutdown.sh

.. note:: If you are running ConfigHub on a reserved port (i.e. 80, and 443), use root access (or ``sudo``).