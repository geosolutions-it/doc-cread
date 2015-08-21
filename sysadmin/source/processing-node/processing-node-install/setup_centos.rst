.. _setup_centos.rst

Installing basic packages
=========================

We are re going to install a minimal CentOS 7 distribution. You can get a copy
of the .iso the image used for the installation `here
<http://mi.mirror.garr.it/mirrors/CentOS/7/isos/x86_64/CentOS-7-x86_64-Minimal-1503-01.iso>`_.

Installing the Operating System
-------------------------------

Boot up the installation DVD and start the `CentOS 7` Installation wizard.

    - Under `Select Date & Time` an set appropriate Date and Time settings
    - Under `Keyboard` and choose the keyboard layout
    - Under `Installation Destination` select the hard disk where CentOS will
      be installed. 
      
      Create a custom partitioning scheme as follows:
      
      +-----------------+----------------+-----------+-------------+
      | Partition Label | Partition Type | Size      | Mount Point |
      +=================+================+===========+=============+
      | boot            | ext3           |   700 MB  | /boot       |
      +-----------------+----------------+-----------+-------------+
      | root            | ext4           |    35 GB  | /           |
      +-----------------+----------------+-----------+-------------+
      | swap            | swap           |     4 GB  |             |
      +-----------------+----------------+-----------+-------------+
    - Under `Networking` configure your network interface according to your infrastructure
      you can either set it to `DHCP` to automatically get all the settings from
      a local DHCP server or configure it by hand.
    - Enable the network interface, then go back to `Select Date & Time` and enable
      NTP synchronization periodically get date and time settings from CentOS servers
    - Click on `Begin Installation`
    - Now set the password for the `root` user. Also click on `User Creation` to
      create the `geosolutions` user.
    -  Wait for the installation process to finish, then reboot your machine

First steps
-----------

Login as `root` user and give the `geosolutions` user administrative privileges
by adding him to the `wheel` group: ::
    usermod -aG wheel geosolutions

SSH access
''''''''''

Allow SSH connections through the firewall
''''''''''''''''''''''''''''''''''''''''''

On CentOS 7 the firewall is enabled by default. To allow SSH clients to connect
to the machine allow incoming connections on port 22::

    firewall-cmd --zone=public --add-port=22/tcp --permanent
    firewall-cmd --zone=public --add-service=ssh --permanent
    firewall-cmd --reload

Disable SSH login for the `root` user
'''''''''''''''''''''''''''''''''''''
.. warning::
    Before you disable root login make sure you are able to login via SSH with
    `geosolutions` user account and you have the privileges to run `sudo su` to
    switch to the `root` user account.

Edit file `/etc/ssh/sshd_config` to disable `root` login via SSH::

    PermitRootLogin no

Public key authentication
'''''''''''''''''''''''''

`Public key authentication`_. is generally consider a safer way to authenticate
users for SSH access. Let's set it up and disable password based authentication

.. _a link: https://en.wikipedia.org/wiki/Public-key_cryptography

First generate a public/private key pair using `ssh-keygen`::

    ssh-keygen

Folllow the procedure, you will end up with your newly generated key under `~/.ssh`
Now copy your `public` (by default it is called id_rsa.pub) key over the CentOS
machine in `/home/geosolutions/.ssh/authorized_keys`. There are several ways to do
it, we are going to use the `ssh-copy-id` tool::

        ssh-copy-id -i ~/.ssh/id_rsa.pub geosolutions@<server-ip-address>

You should now be able to login via SSH as `geosolutions` without been asked for
the password::


    ssh geosolutions@<server-ip-address>

You can now disable password based login over SSH

.. warning::
    Before disabling password authentication make sure you' ve installed your
    public key on the server and you are able to login without password

Edit `/etc/ssh/sshd_config` as follows::

    ...
    RSAAuthentication yes
    ...
    PubkeyAuthentication yes
    ...
    PasswordAuthentication no
    ...
    UsePAM no
    ...

FTP Server
----------

In this section we are going to install `vsftpd` FTP server. As superuser, run::

    yum install vsftpd

Configuration
'''''''''''''

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
'''''''''''''''

You can start and stop vsftpd as follows::

    systemctl start vsftpd
    systemctl stop vsftpd

Enable vsftpd if you want to automatically start at boot time::

    systemctl enable vsftpd

Log rotation
''''''''''''

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
