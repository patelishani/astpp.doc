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


**3. Edit modules.conf and modules.conf.xml**
::

  Enable mod_xml_curl, mod_xml_cdr, mod_perl (If you want to use calling card features)

  sed -i "s#\#xml_int/mod_xml_curl#xml_int/mod_xml_curl#g" /usr/local/src/freeswitch/modules.conf
  sed -i "s#\#mod_xml_cdr#mod_xml_cdr#g" /usr/local/src/freeswitch/modules.conf


.. note:: # add a module by removing '#' comment character at the beginning of the line 
          # remove a module by inserting the '#' comment character at the beginning of the line containing the name of 
            the module to be skipped
          

**4. Compile the Source** 
::

  ./configure -C
          
          
**5. Install Freeswitch with sound files** 
::

   make all install cd-sounds-install cd-moh-install
   make && make install
  
**6. Configure and install mod_perl (Optional)** 
::

   sed -i "s#\#languages/mod_perl#languages/mod_perl#g" /usr/local/src/freeswitch/modules.conf
   ./configure
   make mod_perl-install
  

**7. Set right time in server** 
::

   ntpdate pool.ntp.org


**8. Create symbolic links for Freeswitch executables** 
::

   ln -s /usr/local/freeswitch/bin/freeswitch /usr/local/bin/freeswitch
   ln -s /usr/local/freeswitch/bin/fs_cli /usr/local/bin/fs_cli


**ASTPP Install**

**1. Download ASTPP** 
::

  We assume you have downloaded package from our Download section.
  PATH for download should be /usr/src/
  If not then please download it from here http://astppbilling.org/download/latest.tar.gz

  cd /usr/src 
  wget http://astppbilling.org/download/latest.tar.gz
  tar -xzf latest.tar.gz

**2. Install ASTPP pre-requisite packages using YUM** 
::
  
  yum install -y cpan autoconf automake bzip2 cpio curl curl-devel php php-devel php-common php-cli php-gd php-pear 
  php-mysql php-pdo php-pecl-json mysql mariadb-server mysql-devel libxml2 libxml2-devel openssl openssl-devel
  gettext-devel fileutils gcc-c++ httpd httpd-devel perl-YAML cpan

**3. Install ASTPP Perl packages** 
::
  
  # Enable auto accept for CPAN pacakges.
  perl -MCPAN -e 'my $c = "CPAN::HandleConfig"; $c->load(doit => 1, autoconfig => 1); $c->edit(prerequisites_policy 
  => "follow"); $c->edit(build_requires_install_policy => "yes"); $c->commit' # Install required CPAN packages.
  perl -MCPAN -e "install URI::Escape,JSON,DBI,Time::HiRes,DateTime::Format::Strptime,XML::Simple,CGI,Data::Dumper";

**ASTPP using FreeSWITCH (if you want to use ASTPP with FreeSWITCH)**




