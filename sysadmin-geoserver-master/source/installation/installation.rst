.. _global_setup:

##################
Global setup
##################

The platform-independent binary is a GeoServer web application bundled inside `Jetty`_, a lightweight and portable application server.

.. _Jetty: http://eclipse.org/jetty/

.. note::
   For installing on Linux with an existing application server such as Tomcat, please see the `Web archive` section.

============
Linux Binary
============

Note For installing on Linux with an existing application server such as Tomcat, please see the Web archive section.
The platform-independent binary is a GeoServer web application bundled inside Jetty, a lightweight and portable application server. It has the advantages of working very similarly across all operating systems and is very simple to set up.

installation
------------

1. Make sure you have a Java Runtime Environment (JRE) installed on your system. GeoServer requires a Java 7 environment. The Oracle JRE is preferred, but OpenJDK has been known to work adequately. You can download `JRE 7 from Oracle`_.

.. _JRE 7 from Oracle: http://www.oracle.com/technetwork/java/javase/downloads/

.. note::
   Java 8 is not currently supported.

2. Select the version of GeoServer that you wish to download. If you’re not sure, select Stable.

3. Select Platform Independent Binary on the download page.

4. Download the archive and unpack to the directory where you would like the program to be located.

.. note::
   A suggested location would be /usr/share/geoserver.

5. Add an environment variable to save the location of GeoServer by typing the following command:

.. code:: bash

    echo "export GEOSERVER_HOME=/usr/local/geoserver" >> ~/.profile
    . ~/.profile

6. Make yourself the owner of the geoserver folder. Type the following command in the terminal window, replacing USER_NAME with your own username :

.. code:: bash   

   sudo chown -R USER_NAME /usr/local/geoserver/

7. Add an environment variable to save the location of GeoServer by typing the following command:

.. code:: bash

      echo "export GEOSERVER_HOME=/usr/local/geoserver" >> ~/.profile
      . ~/.profile

8. Make yourself the owner of the geoserver folder, by typing the following command:

.. code:: bash

      sudo chown -R <USERNAME> /usr/local/geoserver/
      where USER_NAME is your user name

9. Start GeoServer by changing into the directory geoserver/bin and executing the startup.sh script:

.. code:: bash

     cd geoserver/bin
     sh startup.sh

10. In a web browser, navigate to http://localhost:8080/geoserver. If you see the GeoServer logo, then GeoServer is successfully installed.

.. image:: img/success.png

To shut down GeoServer, either close the persistent command-line window, or run the shutdown.sh file inside the bin directory.



Uninstallation
--------------

1. Stop GeoServer (if it is running).
2. Delete the directory where GeoServer is installed.

===========
Web Archive
===========

GeoServer is packaged as a standalone servlet for use with existing application servers such as Apache Tomcat and Jetty.

.. note::
   GeoServer has been mostly tested using Tomcat, and so is the recommended application server. Other application servers have been known to work, but are not guaranteed.

Installation
------------

1. Make sure you have a Java Runtime Environment (JRE) installed on your system. GeoServer requires a Java 7 environment. The Oracle JRE is preferred, but OpenJDK has been known to work adequately. You can download JRE 7 from Oracle.

.. note::
   Java 8 is not currently supported.

.. note::
   For more information about Java and GeoServer, please see the section on Java Considerations.

2. Navigate to the GeoServer `Download page`_.

    .. _Download page: http://geoserver.org/download

3. Select Web Archive on the download page.

4. Download and unpack the archive.

5. Deploy the web archive as you would normally. Often, all that is necessary is to copy the geoserver.war file to the application server’s webapps directory, and the application will be deployed.

.. note::
   A restart of your application server may be necessary.


Running
-------

Use your container application’s method of starting and stopping webapps to run GeoServer.

To access the Web Administration Interface, open a browser and navigate to http://SERVER/geoserver . For example, with Tomcat running on port 8080 on localhost, the URL would be http://localhost:8080/geoserver.


Uninstallation
--------------

1. Stop the container application.
2. Remove the GeoServer webapp from the container application’s webapps directory. This will usually include the geoserver.war file as well as a geoserver directory.


