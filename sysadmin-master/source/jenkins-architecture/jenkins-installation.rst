.. _jenkins-installation:

#######################
Unix/Linux Installation
#######################

On Debian-based distributions, such as Ubuntu, you can install Jenkins through apt-get.

Recent versions are available in an `apt repository`_. Older but stable LTS versions are in `this apt repository`_.

.. _apt repository: http://jenkins-ci.org/debian/
.. _this apt repository: http://pkg.jenkins-ci.org/debian-stable/


You need to have a JDK and JRE installed. openjdk-7-jre and openjdk-7-jdk are suggested. As of 2011-08 gcj is known to be problematic - see `<https://issues.jenkins-ci.org/browse/JENKINS-743>`_.

Please make sure to back up any current Hudson or Jenkins files you may have.

============
Installation
============

In order to install jenkins the procedure below has to be followed:

.. code-block:: bash

		wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
		sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
		sudo apt-get update
		sudo apt-get install jenkins
=======
Upgrade
=======

Once installed like this, you can update to the later version of Jenkins (when it comes out) by running the following commands:

.. code-block:: bash

		sudo apt-get update
		sudo apt-get install jenkins

(aptitude or apt-get doesn't make any difference.)

================
Package Features
================


- Jenkins will be launched as a daemon up on start. See :code:`/etc/init.d/jenkins` for more details.
- The 'jenkins' user is created to run this service.
- Log file will be placed in :code:`/var/log/jenkins/jenkins.log`. Check this file if you are troubleshooting Jenkins.
- :code:`/etc/default/jenkins` will capture configuration parameters for the launch like e.g :code:`JENKINS_HOME`
- By default, Jenkins listen on port 8080. Access this port with your browser to start configuration.

.. warning::
   If your :code:`/etc/init.d/jenkins` file fails to start jenkins, edit the :code:`/etc/default/jenkins` to replace the line

   :code:`HTTP_PORT=8080`

   by

   :code:`HTTP_PORT=8081`

   Here, 8081 was chosen but you can put another port available.


 
		 
