.. _install:

Installation
^^^^^^^^^^^^


.. _system-requirements:

System requirements
~~~~~~~~~~~~~~~~~~~

The ConfigHub server application has the following prerequisites:

* Some modern Linux distribution (Debian Linux, Ubuntu Linux, or CentOS recommended)
* MySQL 5.0 or later (latest stable version is recommended)
* Oracle Java SE 8 or later (latest stable update is recommended)


Download and Install
~~~~~~~~~~~~~~~~~~~~

* Download and install Java8 to your localhost.  Set the ``JAVA_HOME`` environment variable to Java's bin directory::

   export JAVA_HOME=/path/to/java8/bin

* `Download <https://www.confighub.com/download>`_ the latest version of ConfigHub:

* Uncompress the downloaded file::

   tar -xzvf confighub-<version>.tar.gz


Manual Configuration
~~~~~~~~~~~~~~~~~~~~

* Edit the configuration file ``confighub.properties`` in confighub-<version> directory.
* Each configuration parameter has to be specified.

.. code-block:: bash

   # Settings for the primary ConfigHub Database.
   db.main.host = 127.0.0.1
   db.main.port = 3306
   db.main.name = ConfigHub
   db.main.username =
   db.main.password =
   db.main.useSSL = false

   # Settings for the database that will store all incoming client (API) requests.
   db.api.host = 127.0.0.1
   db.api.port = 3306
   db.api.name = ConfigHubClientRequests
   db.api.username =
   db.api.password =
   db.api.useSSL = false

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



ConfigHub License File
~~~~~~~~~~~~~~~~~~~~~~

If you are using a Free ConfigHub version, you do not need a license file.

For Enterprise license holders, place your license file "license.json" received from ConfigHub into the
confighub-<version> directory (same directory as the confighub.properties file.)




Starting and Stopping ConfigHub Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Start ConfigHub::

   confighub-<version>/server/bin/startup.sh

* Stop ConfigHub::

   confighub-<version>/server/bin/shutdown.sh

.. note:: If you are running ConfigHub on a reserved port (i.e. 80, and 443), use root access (or ``sudo``).