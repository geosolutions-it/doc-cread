#####################
Updating Applications
#####################

Updating Jenkins
================

   You may want to take a **backup** before upgrading. There are several ways to
   to backup Jenkins depending on your needs. From manual copy of Jenkins configuration
   files, jobs folders and workspaces to automated backups using Jenkins plugins.
   ( See `thinBackup <https://wiki.jenkins-ci.org/display/JENKINS/thinBackup>`_
   and `Backup Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Backup+Plugin>`_
   for an example of plugin based backups ).

Updating Jenkins is pretty straight forward.

Download the new .war from Jenkins official `web site <https://jenkins-ci.org/>`_

Stop the running instance of jenkins
::
    systemctl stop tomcat@jenkins

Replace the old .war file
::
    cp jenkins.war /var/lib/tomcat/jenkins/webapps/jenkins.war

And restart Jenkins
::
    systemctl start tomcat@jenkins

Updating Jenkins Plugins
========================

From Jenkins user interface click on `Manage Jenkins` then `Manage Plugins` you will
see lists of available and installed plugins as well as a list of available updates
for the installed plugin.

Jenkins will periodically look for available updates for the plugins you can also
ask Jenkins to check for available updates clicking on `Check Now` at the bottom
of the page.

Select the plugins you want to update and click on `Download now and install after restart`.

Then restart Jenkins.


.. note::
    When you update Jenkins to a newer version plugins bundled with Jenkins will normally
    be updated too, unless they have been manually updated. In that case Jenkins will
    mark the plugins as `pinned` and will not automatically overwritten. For more
    information see `here <https://wiki.jenkins-ci.org/display/JENKINS/Pinned+Plugins>`_

Updating Apache HTTP server
===========================

We installed Apache HTTP server via the official CentOS repositories. You can update
Apache using `yum`
::
    yum check-update
    yum update httpd

Updating Apache Tomcat
======================

Download the Gzip compressed folder of the desired version of Tomcat from the
official `web site <http://tomcat.apache.org/>`_
::
    wget http://it.apache.contactlab.it/tomcat/.../apache-tomcat-XXX.tar.gz

Extract it
::
    tar xvf apache-tomcat-XXX.tar.gz

And move it to under `/opt/`
::
    mv apache-tomcat-XXX /opt/

Then stop all running instances of tomcat. For example, to stop Jenkins:
::
    systemctl stop tomcat@jenkins

And replace the symbolic link pointing to the old version of Tomcat with a new
link pointing to the one you are installing
::
    rm /opt/tomcat
    ln -s /opt/apache-tomcat-XXX /opt/tomcat

Restart all Tomcat instances and make sure all services are running as expected.
Once you checked that all the services are working, you can delete the old version
Tomcat from `/opt`
::
    rm -rf /opt/apache-tomcat-YYY
