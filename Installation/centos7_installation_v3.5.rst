============================
CentOs 7 Installation V3.5
============================

**Install base packages**
::

 yum update
 yum groupinstall "Development tools" -y
 
 #Enable epel and freeswitch repository
 yum install epel-release
 rpm -Uvh http://files.freeswitch.org/freeswitch-release-1-6.noarch.rpm
 yum update

|

**Install Freeswitch**

**1. Install Freeswitch pre-requisite packages**


::

 #Install dependencies for freeswitch
 yum install -y wget git autoconf automake expat-devel yasm gnutls-devel libtiff-devel libX11-devel unixODBC-devel python-devel
 zlib-devel alsa-lib-devel libogg-devel libvorbis-devel uuid-devel @development-tools gdbm-devel db4-devel libjpeg libjpeg-deve
|


