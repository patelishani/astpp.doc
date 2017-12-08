===================
Service Monitoring
===================

Monit is a small Open Source utility for managing and monitoring systems. Monit conducts automatic maintenance and repair and can execute meaningful causal actions in error situations.  

For ASTPP we can configure apache,freeswitch and mysql services to monitor.

**Installation**
::
    For CentOS
    yum install monit

    For Debian
    apt-get install monit




Configurations:
***************

**Enable Web Interface in Monit**
::
    Monit also provided an web interface to view services and processes status. To enable monit web interface, 
    edit configuration file ( For CentOS /etc/monit.conf & For Debian System /etc/monit/monitrc ) and modify following 
    lines as per your server information's

    set httpd port 2812 and
    use address localhost
    allow localhost
    allow admin:monit
    allow @monit
    allow @users readonly









