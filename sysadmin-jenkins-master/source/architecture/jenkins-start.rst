.. _jenkins-start:

##############################
Starting and Accessing Jenkins
##############################

================
Starting Jenkins
================

The easiest way to execute Jenkins is through the built in Jetty servlet container. You can execute Jenkins like this:

.. code-block:: bash

		$ java -jar jenkins.war

Of course, you probably want to send the output of Jenkins to a log file, and if you're on Unix, you probably want to use nohup:

.. code-block:: bash

		$ nohup java -jar jenkins.war > $LOGFILE 2>&1

=================
Accessing Jenkins
=================

To see Jenkins, simply bring up a web browser and go to URL http://myServer:8080 where myServer is the name of the system running Jenkins.

=======================
Command Line Parameters
=======================

Jenkins normally starts up using port 8080. However, if you have other web services starting up you might find that this port is already taken. You can specify a different port by using :code:`--httpPort=$HTTP_PORT` where :code:`$HTTP_PORT` is the port you want Jenkins to run on. Other command line parameters include:


+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Command Line Parameter                                                                                | Description                                                                                                                                                                                                                                               |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| --httpPort=$HTTP_PORT                                                                                 | Runs Jenkins listener on port $HTTP_PORT using standard http protocol. The default is port 8080. To disable (because you're using https), use port -1.                                                                                                    |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| --httpListenAddress=$HTTP_HOST                                                                        | Binds Jenkins to the IP address represented by $HTTP_HOST. The default is 0.0.0.0 — i.e. listening on all available interfaces.                                                                                                                           |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| For example, to only listen for requests from localhost, you could use: --httpListenAddress=127.0.0.1 |                                                                                                                                                                                                                                                           |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| --httpsPort=$HTTP_PORT                                                                                | Uses HTTPS protocol on port $HTTP_PORT                                                                                                                                                                                                                    |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| --httpsListenAddress=$HTTPS_HOST                                                                      | Binds Jenkins to listen for HTTPS requests on the IP address represented by $HTTPS_HOST.                                                                                                                                                                  |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| --prefix=$PREFIX                                                                                      | Runs Jenkins to include the $PREFIX at the end of the URL. For example, to make Jenkins accessible at http://myServer:8080/jenkins, set --prefix=/jenkins                                                                                                 |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| --ajp13Port=$AJP_PORT                                                                                 | Runs Jenkins listener on port $AJP_PORT using standard AJP13 protocol. The default is port 8009. To disable (because you're using https), use port -1.                                                                                                    |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| --ajp13ListenAddress=$AJP_HOST                                                                        | Binds Jenkins to the IP address represented by $AJP_HOST. The default is 0.0.0.0 — i.e. listening on all available interfaces.                                                                                                                            |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| --argumentsRealm.passwd.$ADMIN_USER                                                                   | Sets the password for user $ADMIN_USER. If Jenkins security is turned on, you must log in as the $ADMIN_USER in order to configure Jenkins or a Jenkins project. NOTE: You must also specify that this user has an admin role. (See next argument below). |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| --argumentsRealm.roles.$ADMIN_USER=admin                                                              | Sets that $ADMIN_USER is an administrative user and can configure Jenkins if Jenkins' security is turned on. See Securing Jenkins for more information.                                                                                                   |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -Xdebug -Xrunjdwp:transport=dt_socket,address=$DEBUG_PORT,server=y,suspend=n                          | Sets debugging on and you can access debug on $DEBUG_PORT.                                                                                                                                                                                                |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -logfile=$LOG_PATH/winstone_`date +"%Y%m-%d_%H-%M"`.log                                               | Logging to desired file                                                                                                                                                                                                                                   |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| -XX:PermSize=512M -XX:MaxPermSize=2048M -Xmn128M -Xms1024M -Xmx2048M                                  | referring to these options for Oracle Java                                                                                                                                                                                                                |
+-------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
.. warning::

   Be Careful with Command Line Parameters.
   Jenkins ignores command line parameters it doesn't understand instead of producing an error. Be careful when using command line parameters and make sure you have the correct spelling. For example, the parameter needed for defining the Jenkins administrative user is --argumentsRealm and not --argumentRealm.

Init script example
-------------------

.. note::
   	The following script is for Ubuntu based systems.

.. code-block:: bash

		#!/bin/sh
		DESC="Jenkins CI Server"
		NAME=jenkins
		PIDFILE=/var/run/$NAME.pid
		RUN_AS=jenkins
		COMMAND=/usr/bin/java -- -jar /home/jenkins/jenkins.war

		d_start() {
		         start-stop-daemon --start --quiet --background --make-pidfile --pidfile $PIDFILE --chuid $RUN_AS --exec $COMMAND
		}

		d_stop() {
		          start-stop-daemon --stop --quiet --pidfile $PIDFILE
		          if [ -e $PIDFILE ]
		              then rm $PIDFILE
		          fi
		}

		case $1 in
		   start)
	           echo -n "Starting $DESC: $NAME"
	           d_start
	           echo "."
	           ;;
	           stop)
	           echo -n "Stopping $DESC: $NAME"
	           d_stop
	           echo "."
	           ;;
	          restart)
	          echo -n "Restarting $DESC: $NAME"
	          d_stop
	          sleep 1
	          d_start
	          echo "."
	          ;;
	          *)
	          echo "usage: $NAME {start|stop|restart}"
	          exit 1
	          ;;
		esac
		exit 0
