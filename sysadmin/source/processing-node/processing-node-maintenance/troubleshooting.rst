.. _troubleshooting:

###############
Troubleshooting
###############

=======
Jenkins
=======

Jenkins is unreacheable
'''''''''''''''''''''''


Login on the server with `sudo` privileges and look for a running Tomcat instance,
you should see an instance of Tomcat running Jenkins::

    ps aux | grep tomcat
    tomcat   32662  0.1 10.6 3110092 412612 ? Sl   ago07   8:43 ...-Dcatalina.base=/var/lib/tomcat/jenkins -Dcatalina.home=/opt/tomcat...

If that is not the case, check the status
of Jenkins service first::

    systemctl status tomcat@jenkins

The status should be `active`::

    ...
    Active: active (running) since gio 2015-08-06 15:10:24 CEST; 3 days ago
    ...

If you read `Not Running` instead, try to start it manually::

    systemctl start tomcat@jenkins

Wait a few seconds and check the status again::

    systemctl status tomcat@jenkins

If the service is marked as `active`, use your browser to connect to Jenkins web UI
and check that Jenkins is up and running and working as expected.

If that is the case then make sure that you enabled automatic startup of Jenkins
as described in "Jenkins Installation".

If Jenkins is running but you are still unable to connect to the web UI then login
on the server and try to connect to Jenkins locally using a command line browser like
`lynx <https://en.wikipedia.org/wiki/Lynx_(web_browser)>`_ ::

    lynx http://localhost:8080/jenkins

If you are able to connect to Jenkins locally, then check your firewall configuration
first and make sure it allows incoming requests on port 80. Then check your Apache
HTTP server configuration.

Jenkins is failing to start
'''''''''''''''''''''''''''

To troubleshoot startup problems first read the log file located at `/var/lib/tomcat/jenkins/logs/catalina.out`.
containing informations about Jenkins startup process. Make a backup `catalina.out`,
delete it and try to start Jenkins::

    mv /var/lib/tomcat/jenkins/logs/catalina.out /var/lib/tomcat/jenkins/logs/catalina.bkp
    systemctl start tomcat@jenkins

Follow the startup process::

    tail -f /var/lib/tomcat/jenkins/logs/catalina.out

Or read the entire log file when startup process is finished or failed::

    less /var/lib/tomcat/jenkins/logs/catalina.out

If you find `catalina.out` to be empty or missing and Jenkins still not running,
then it is likely that there is a problem either with Tomcat itself or the startup
script.

run::

    systemctl status tomcat@jenkins

and::

    journalctl -xn

To get informations about the early startup process of Jenkins

Reset Jenkins Administrator Password
''''''''''''''''''''''''''''''''''''

In this scenario you will have to temporarily disable Jenkins security, delete the
administrator user account and recreate it.

.. warning::
    We are going to disable Jenkins security make sure Jenkins is not open to the public
    and only accessible locally

Jenkins configuration files, as well as jobs config files and plugins are stored
in the $JENKINS_HOME folder, under `/usr/share/tomcat/.jenkins/`

Navigate to `/usr/share/tomcat/.jenkins/` and edit Jenkins global configuration file
`config.xml`.

Set `useSecurity` to `false` and comment out the `authorizationStrategy` section::

    <useSecurity>false</useSecurity>
    <!--
    <authorizationStrategy class="hudson.security.GlobalMatrixAuthorizationStrategy">
      <permission>com.cloudbees.plugins.credentials.CredentialsProvider.Create:geosolutions</permission>
      <permission>com.cloudbees.plugins.credentials.CredentialsProvider.Delete:geosolutions</permission>
      ....
    </authorizationStrategy>
    -->
    ...

Now start Jenkins. This time you will not be asked to login and you will be able
to recreate the admin user.

Then edit `/usr/share/tomcat/.jenkins/config.xml` again and restore the original configuration::

    <useSecurity>true</useSecurity>
    <authorizationStrategy class="hudson.security.GlobalMatrixAuthorizationStrategy">
      <permission>com.cloudbees.plugins.credentials.CredentialsProvider.Create:geosolutions</permission>
      <permission>com.cloudbees.plugins.credentials.CredentialsProvider.Delete:geosolutions</permission>
      ....
    </authorizationStrategy>
    ...

Restart Jenkins::

    systemctl restart tomcat@jenkins
