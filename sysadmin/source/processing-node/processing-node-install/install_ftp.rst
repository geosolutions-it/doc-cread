.. _setup_centos_ftp.rst

##########
FTP Server
##########

In this section we are going to install `vsftpd` FTP server.

As superuser, run::

    yum install vsftpd

Configuration
=============

Now edit the configuration file located at `/etc/vsftpd/vsftpd.conf` and set the
following options::

    anonymous_enable=NO
    local_enable=YES
    write_enable=YES
    chroot_local_user=NO
    local_umask=022
    dirmessage_enable=YES
    xferlog_enable=YES
    connect_from_port_20=YES
    xferlog_std_format=YES
    listen=NO
    listen_ipv6=YES
    pam_service_name=vsftpd
    userlist_enable=YES
    userlist_deny=NO
    tcp_wrappers=YES

With this configuration only the users listed in `/etc/vsftpd/user` are allowed to
connect via FTP, edit the file::

    vim /etc/vsftpd/user_list_allowed

and add `geosolutions` user::

    geosolutions

Manage `vsftpd`
===============

You can start and stop vsftpd as follows::

    systemctl start vsftpd
    systemctl stop vsftpd

Enable vsftpd if you want to automatically start at boot time::

    systemctl enable vsftpd

Log rotation
============

Over time, log file can grow pretty large. To avoid having the filesystem filled up
with log files we are going to use `Logrotate` to periodically truncate and/or
compress them.

Edit the logrotate configuration file for vsftpd under `/etc/logrotate.d/vsftpd` as follows::

    /var/log/vsftpd.log {
        # ftpd doesn't handle SIGHUP properly
        daily
        rotate 10
        nocompress
        missingok
        maxsize 5M
        create 640 root root
    }

    /var/log/xferlog {
        # ftpd doesn't handle SIGHUP properly
        daily
        rotate 10
        nocompress
        missingok
        maxsize 5M
        create 640 root root
    }

Then add an entry in the `crontab` to run logrotate periodically:
run `crontab -e` and add this line at the bottom::

    ...
    0 * * * * /usr/sbin/logrotate /etc/logrotate.d/vsftpd
