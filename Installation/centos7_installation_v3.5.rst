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
 compat-libtermcap ncurses ncurses-devel ntp screen sendmail sendmail-cf gcc-c++ @development-tools bison bzip2 curl curl-devel 
 dmidecode git make mysql-connector-odbc openssl-devel unixODBC zlib pcre-devel speex-devel sqlite-devel ldns-devel libedit-
 devel bc e2fsprogs-devel libcurl-devel libxml2-devel libyuv-devel opus-devel libvpx-devel libvpx2* libdb4* libidn-devel unbou-
 nd devel libuuid-devel lua-devel libsndfile-devel


**2. Download latest freeswitch version**
::
  
  cd /usr/local/src
  git config --global pull.rebase true

  #Clone freeswitch version 1.6.8 from git 
  git clone -b v1.6.19 https://freeswitch.org/stash/scm/fs/freeswitch.git
  cd freeswitch
  ./bootstrap.sh -j

