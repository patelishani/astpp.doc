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

**1. Configure freeswitch startup script** 
::

  cp /usr/src/latest/freeswitch/init/freeswitch.centos.init /etc/init.d/freeswitch
  chmod 755 /etc/init.d/freeswitch
  chmod +x /etc/init.d/freeswitch
  chkconfig --add freeswitch
  chkconfig --level 345 freeswitch on
  mkdir /var/run/freeswitch


**2. Configure ASTPP with freeswitch** 
::

    #Create directory structure for ASTPP
    mkdir -p /var/lib/astpp/
    mkdir -p /var/log/astpp/
    mkdir -p /usr/local/astpp/
    mkdir -p /var/www/

    #Setting permisssion
    chown -Rf apache.apache /var/lib/astpp/
    chown -Rf apache.apache /var/log/astpp/
    chown -Rf apache.apache /usr/local/astpp/
    chown -Rf apache.apache /var/www/
    chown -Rf apache.apache /var/www/cgi-bin/

    #Setting up cgi-bin
    cp -rf /usr/src/latest/scripts/*.pl /usr/local/astpp/
    cp -rf /usr/src/latest/freeswitch/astpp /var/www/cgi-bin/
    chmod -Rf 777 /var/www/cgi-bin/astpp

    cp /usr/src/latest/freeswitch/astpp-callingcards.pl /usr/local/freeswitch/scripts/astpp-callingcards.pl
    cp -rf /usr/src/latest/sounds/*.wav /usr/local/freeswitch/sounds/en/us/callie/
    chmod -Rf 777 /usr/local/freeswitch/sounds/en/us/callie/

**Install ASTPP web interface** 
::

   mkdir -p /var/lib/astpp
   cp /usr/src/latest/astpp_confs/sample.astpp-config.conf /var/lib/astpp/astpp-config.conf

   mkdir -p /var/www/html/astpp
   cp -rf /usr/src/latest/web_interface/astpp/* /var/www/html/astpp/
   cp /usr/src/latest/web_interface/astpp/htaccess /var/www//html/astpp/.htaccess

   chown -Rf apache.apache /var/www/html/astpp
   cp /usr/src/latest/web_interface/apache/astpp.conf /etc/httpd/conf.d/astpp.conf

   #apply security policy 
   sed -i "s/SELINUX=enforcing/SELINUX=disabled/" /etc/sysconfig/selinux
   sed -i "s/SELINUX=enforcing/SELINUX=disabled/" /etc/selinux/config
   /etc/init.d/iptables stop
   chkconfig iptables off
   setenforce 0

   chmod -Rf 777 /var/www/html/astpp
   touch /var/log/astpp/astpp.log


**Install ASTPP Database**
::

   #Restart mysql service
   systemctl start mariadb
   mysql -uroot -e "UPDATE mysql.user SET password=PASSWORD('<MYSQL_ROOT_PASSWORD>') WHERE user='root'; FLUSH PRIVILEGES;"

   # Create database astpp
   mysql -uroot -p<MYSQL_ROOT_PASSWORD> -e "create database astpp;"
   mysql -uroot -p<MYSQL_ROOT_PASSWORD> -e "CREATE USER 'astppuser'@'localhost' IDENTIFIED BY '<ASTPP_USER_PASSWORD>';"
   mysql -uroot -p<MYSQL_ROOT_PASSWORD> -e "GRANT ALL PRIVILEGES ON \`astpp\` . * TO 'astppuser'@'localhost' WITH GRANT        OPTION;FLUSH PRIVILEGES;"
   mysql -uroot -p<MYSQL_ROOT_PASSWORD> astpp < /usr/src/latest/sql/astpp-2.0.sql
   mysql -uroot -p<MYSQL_ROOT_PASSWORD> astpp < /usr/src/latest/sql/astpp-upgrade-rates-2.0.sql
   mysql -uroot -p<MYSQL_ROOT_PASSWORD> astpp < /usr/src/latest/sql/astpp-upgrade-2.1.sql
   mysql -uroot -p<MYSQL_ROOT_PASSWORD> astpp < /usr/src/latest/sql/astpp-upgrade-2.2.sql
   mysql -uroot -p<MYSQL_ROOT_PASSWORD> astpp < /usr/src/latest/sql/astpp-upgrade-2.3.sql


**ASTPP Freeswitch Configuration**
::

  cp latest/freeswitch/conf/autoload_configs/* /usr/local/freeswitch/conf/autoload_configs/

  Enable mod_xml_curl, mod_xml_cdr, mod_cdr_csv, mod_perl in /usr/local/freeswitch/conf/autoload_configs/modules.conf.
  xml file.


**Finalize Installation & Start Services**
::

   #Open php short tag
   sed -i "s#short_open_tag = Off#short_open_tag = On#g" /etc/php.ini

   #Setup port for ASTPP
   yum update		
   mkdir -p /etc/httpd/sites-available
   mkdir -p /etc/httpd/sites-enabled
   mv /etc/httpd/conf.d/astpp.conf /etc/httpd/sites-available/.
   ln -s /etc/httpd/sites-available/astpp.conf /etc/httpd/sites-enabled/astpp.conf
   sed -i "$ a IncludeOptional sites-enabled/*.conf" /etc/httpd/conf/httpd.conf

   #Configure security policy
   sed -i "s/SELINUX=enforcing/SELINUX=disabled/" /etc/sysconfig/selinux
   sed -i "s/SELINUX=enforcing/SELINUX=disabled/" /etc/selinux/config
   setenforce 0

   #Install cpan modules
   cpan -fi DBI
   cpan -fi CGI
   yum install perl-XML-Simple

   #Configure services for startup
   systemctl enable httpd
   apachectl restart
   systemctl start httpd
   systemctl start mariadb
   systemctl start freeswitch
   systemctl stop firewalld
   chkconfig --levels 345 httpd on
   chkconfig --levels 345 mariadb on
   chkconfig --levels 345 freeswitch on
   chkconfig --levels 123456 firewalld off

**Setup cron**
::
 
    # Generate Invoice   
    0 1 * * * cd /var/www/html/astpp/cron/ && php cron.php GenerateInvoice

    # Low balance notification
    0 1 * * * cd /var/www/html/astpp/cron/ && php cron.php UpdateBalance

    # Low balance notification
    0 0 * * * cd /var/www/html/astpp/cron/ && php cron.php LowBalance

    # Low credit notification
    0 0 * * * cd /var/www/html/astpp/cron/ && php cron.php LowCredit

    # Update currency rate
    0 0 * * * cd /var/www/html/astpp/cron/ && php cron.php CurrencyUpdate

**Setup database credential and change other require things in astpp configuration file**
::

   vim /var/lib/astpp/astpp-config.conf

 
   #Restart your server and verify your installation
   init 6



.. note:: 
     You are done with GUI installation. Enjoy :)
     Visit the astpp admin page in your web browser. It can be found here: http://server_ip:8081/ Please change the
     ip address depending upon your box. The default username and password is “admin”. 
     Note : In case of any issue please refer apache error log.

.. note:: 
     If you have any other question(s) then please contact us on sales@inextrix.com or post your questions(s) 
     in https://groups.google.com/forum/#!forum/astpp.

