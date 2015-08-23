
##########################
Install Apache http server
##########################

Install base package ::

    yum install httpd

and additional modules::

    yum install httpd mod_ssl mod_proxy_html

Firewall configuration
======================

Allow requests on port 80 through the firewall::

    firewall-cmd --zone=public --add-port=80/tcp --permanent
    firewall-cmd --zone=public --add-service=http --permanent
    firewall-cmd --reload

Apache Configuration
====================

We' re going to use Apache as a reverse proxy. All incoming requests on port 80
will be processed by Apache routed to Jenkins on port 8080

Create the file ``/etc/httpd/conf.d/reverse-proxy.conf`` with the following content to setup the reverse proxy::

    <VirtualHost *:80>

        ProxyRequests Off
        AllowEncodedSlashes NoDecode

        ServerName processing.geo-solutions.it
        ServerAdmin info@geo-solutions.it

        ProxyPass /jenkins http://localhost:8080/jenkins nocanon connectiontimeout=5 timeout=30
        ProxyPassReverse /jenkins http://localhost:8080/jenkins
        AllowEncodedSlashes Nodecode

    	<Proxy http://localhost:8080/jenkins*>
            Order deny,allow
            Allow from all
        </Proxy>

    </VirtualHost>

Apache start and stop
=====================

To start and stop Apache, run::

    systemctl start httpd
    systemctl stop httpd

To automatically start Apache at boot, run::

    systemctl enable httpd

Log Rotation
============

Edit the configuration file for logrotate to rotate Apache log files
( /etc/logrotate.d/httpd ) as follows::

    /var/log/httpd/*log {
        daily
        maxsize 100M
        rotate 14
        missingok
        create 644 root root
        notifempty
        sharedscripts
        compress
        delaycompress
        postrotate
            /bin/systemctl reload httpd.service > /dev/null 2>/dev/null || true
        endscript
    }

And add the following line to the crontab::

    crontab -e
    
    0 * * * * /usr/sbin/logrotate /etc/logrotate.d/httpd
