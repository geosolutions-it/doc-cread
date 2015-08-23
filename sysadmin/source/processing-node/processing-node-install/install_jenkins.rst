Applications Installation and configuration
===========================================

Tomcat and Jenkins
------------------

Tomcat Installation
'''''''''''''''''''

We are going to run `Jenkins` as a `Tomcat` instance. Let's download and
install `Tomcat` first::

    wget http://it.apache.contactlab.it/tomcat/tomcat-7/v7.0.63/bin/apache-tomcat-7.0.63.tar.gz
    tar xvf /apache-tomcat-7.0.63.tar.gz
    mv apache-tomcat-7.0.63 /opt
    ln -s /opt/apache-tomcat-7.0.63 /opt/tomcat

Then prepare a clean instance called `base` to be used as a template for all tomcat instances::

    mkdir -p /var/lib/tomcat/base/{bin,conf,logs,temp,webapps,work}\
    cp -r /opt/tomcat/conf/* /var/lib/tomcat/base/conf/*

And fix the permissions on the files::

    chown -R tomcat:tomcate /opt/apache*
    chown -R tomcat:tomcat /var/lib/tomcat

Instance manager script
'''''''''''''''''''''''

To manage our Tomcat instances create the file /etc/systemd/system/tomcat\@.service
with the following content::

    [Unit]
    Description=Tomcat %I
    After=network.target

    [Service]
    Type=forking
    User=tomcat
    Group=tomcat

    Environment=CATALINA_PID=/var/run/tomcat/%i.pid
    #Environment=TOMCAT_JAVA_HOME=/usr/java/default
    Environment=CATALINA_HOME=/opt/tomcat
    Environment=CATALINA_BASE=/var/lib/tomcat/%i
    Environment=CATALINA_OPTS=

    ExecStart=/opt/tomcat/bin/startup.sh
    ExecStop=/opt/tomcat/bin/shutdown.sh
    #ExecStop=/bin/kill -15 $MAINPID

    [Install]
    WantedBy=multi-user.target

Jenkins Installation
''''''''''''''''''''

Prepare a new instance of Tomcat for Jenkins::

    mkdir -p /var/lib/tomcat/jenkins
    cp -r /var/lib/tomcat/base/* /var/lib/tomcat/jenkins/*
    chown -R tomcat:tomcat /var/lib/tomcat

Then download and deploy the latest LTS ( at the time of writing 1.609.2) war for Jenkins::

    wget http://mirrors.jenkins-ci.org/war-stable/latest/jenkins.war
    chown tomcat:tomcat ./jenkins.war
    mv jenkins.war /var/lib/tomcat/jenkins/webapps/

.. _jenkins-auto-startup:

Now enable automatic startup creating this symlink::

    ln-s /etc/systemd/system/tomcat\@.service /usr/lib/systemd/system/multi-user.target.wants/tomcat@jenkins.service

Basic installation is finished. We can now start Jenkins. By default Jenkins will
listen to requests on port 8080. To test the installation temporarily open port
8080 in the firewall::

    firewall-cmd --zone=public --add-port=8080/tcp
    firewall-cmd --zone=public --add-service=http
    firewall-cmd --reload

Start Jenkins::

    systemctl start tomcat@jenkins

You should be able to access Jenkins via HTTP on port 8080. Open http://<server-ip-or-hostname>:8080/jenkins
with your favourite browser.

To stop Jenkins, run::

    systemctl stop tomcat@jenkins

Jenkins basic configuration
'''''''''''''''''''''''''''

Let's first enable user authentication.
    - Start Jenkins and browse to Jenkins web user interface again
    - Click on "Manage Jenkins", then "Configure Global Security"
    - Set the "Enable securiy" and "Use Jenkin's own database" options
    - Click "Save" at the bottom of the page

Create a new user
    - Go back to “Manage Jenkins” and click on “Manage Users”, then "Add User"
    - Create a `geosolutions` user

Restict access to Jenkins
    - Go back to “Configure Global Security”, under "Authorization" select “Matrix based security”
    - Add the user 'geosolutions' to the matrix and check all the boxes for it
      (`geosolutions` will be used ad and admin user for Jenkins)
    - For the `Anonymous` user check the `Read` box in the `Overall` column and `Discover`
      and `Read` boxes under the `Job` column to allow unregistered users to view all the
      jobs.

Install Git
-----------

Jenkins is able to connect to various `Version Contol Systems` and look for changes
in files to trigger build jobs. `Git` is a popular `VCS` and by installing Git, Jenkins
will be able (after installing Jenkins plugins) to access `Git repositories` either
local or hosted ones like `Github` repositories.

In the terminal type the following to install Git::

    yum install git

Install Jenkins Plugins
-----------------------

Go back to the Jenkins UI to install extra plugins. Under “Manage Jenkins” click
on “Manage Plugins” and install the following:
    - "Git Plugin"
    - "GitHub plugin"

Then restart Jenkins and create a new Jenkins job. You will see new options
available related to Git repositories and `Github`.

Log Rotation
------------

To avoid having the filesystem filled up with log files we are going to use
`Logrotate` to periodically truncate and/or compress Jenkins log files.

Edit the logrotate configuration file for vsftpd under `/etc/logrotate.d/jenkins`
as follows::

    /var/lib/tomcat/jenkins/logs/catalina.out {
            daily
            missingok
            maxsize 5M
            rotate 10
            compress
            delaycompress
            create 644 tomcat tomcat
    }

Then add the following line to the crontab::

    crontab -e
    …
    0 * * * * /usr/sbin/logrotate /etc/logrotate.d/jenkins
    …
