.. _install:

Local ConfigHub Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^


.. _system-requirements:

===================
System requirements
===================

The ConfigHub server application has the following prerequisites:

* Some modern Linux distribution (Debian Linux, Ubuntu Linux, or CentOS recommended)
* MySQL 5.0 or later (latest stable version is recommended)
* Oracle Java SE 8 or later (latest stable update is recommended)


Download and Install
--------------------

    - Download and install Java8 to your local host, and set the environment variable
      JAVA_HOME to the location of the Java's bin directory.

    - `Download <https://www.confighub.com/download>`_ the latest version of ConfigHub:

    - Uncompress the downloaded file
      tar -xzvf confighub-<version>.tar.gz


Manual Configuration
--------------------

    - Edit the configuration file "confighub.properties" in confighub-<version> directory.
    - Each configuration parameter has to be specified.


ConfigHub License File
----------------------

    - Place your license file "license.json" received from ConfigHub into the confighub-<version> directory
      (same directory as the confighub.properties file.)


Starting and Stopping ConfigHub Service
---------------------------------------

    - To start ConfigHub, run confighub-<version>/server/bin/startup.sh
    - To stop ConfigHub, run confighub-<version>/server/bin/shutdown.sh

    If you are running ConfigHub on a reserved port (i.e. 80, and 443), use root access (or sudo).