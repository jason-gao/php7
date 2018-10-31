# centos 安装php7.3.0

* yum -y install libxml2 libxml2-devel openssl openssl-devel curl-devel libjpeg-devel libpng-devel freetype-devel libmcrypt-devel libzip-devel cmake

* cd /usr/local/src
* wget -c https://github.com/php/php-src/archive/php-7.3.0RC4.tar.gz
* cd /usr/local/src && tar -zxvf php-7.3.0RC4.tar.gz
* cd /usr/local/src/php-src-php-7.3.0RC4
* ./buildconf，如提示autoconf版本过低，参考error进行升级，如正确会生成confiure文件
* ./buildconf --force

* error
buildconf: autoconf version 2.63 found.
           You need autoconf version 2.68 or newer installed
           to build PHP from Git.
make: *** [buildmk.stamp] Error 1

```

./configure --prefix=/usr/local/php7.3.0 \
--with-config-file-path=/usr/local/php7.3.0/etc \
--with-config-file-scan-dir=/usr/local/php7.3.0/etc/php.d \
--enable-mysqlnd \
--with-mysqli \
--with-pdo-mysql \
--enable-fpm \
--with-fpm-user=www \
--with-fpm-group=www \
--with-gd \
--with-iconv \
--with-zlib \
--enable-xml \
--enable-shmop \
--enable-sysvsem \
--enable-inline-optimization \
--enable-mbregex \
--enable-mbstring \
--enable-ftp \
--with-openssl \
--enable-pcntl \
--enable-sockets \
--with-xmlrpc \
--enable-zip \
--enable-soap \
--without-pear \
--with-gettext \
--enable-session \
--with-curl \
--with-jpeg-dir \
--with-freetype-dir \
--enable-opcache \
--enable-bcmath \
--with-libzip=/usr/local/lib64 \


```
* error
    * configure: error: system libzip must be upgraded to version >= 0.11
        * yum remove libzip
        * cd /usr/local/src && wget -c https://libzip.org/download/libzip-1.5.1.tar.gz
        * tar -zxvf libzip-1.5.1.tar.gz && cd libzip-1.5.1
        * rm -rf build && mkdir build && cd build && cmake .. && make && make install
            * CMake 3.0.2 or higher is required.  You are running version 2.8.12.2
            * cd /usr/local/src && wget -c https://cmake.org/files/v3.6/cmake-3.6.2.tar.gz
            * tar -zxvf cmake-3.6.2.tar.gz && cd cmake-3.6.2/
            * ./configure && gmake && gmake install
            * /usr/local/bin/cmake --version
            * yum remove cmake -y
            * ln -s /usr/local/bin/cmake /usr/bin/
            * cmake --version
        * -- Installing: /usr/local/bin/zipcmp
          -- Set runtime path of "/usr/local/bin/zipcmp" to ""
          -- Installing: /usr/local/bin/zipmerge
          -- Set runtime path of "/usr/local/bin/zipmerge" to ""
          -- Installing: /usr/local/bin/ziptool
          -- Set runtime path of "/usr/local/bin/ziptool" to ""
    * configure: error: off_t undefined; check your library configuration
              ```
              echo '/usr/local/lib64
              /usr/local/lib
              /usr/lib
              /usr/lib64'>>/etc/ld.so.conf&&ldconfig -v
              ```
        * https://segmentfault.com/q/1010000007346459
        
* make -j 2
* make install

```

Installing shared extensions:     /usr/local/php7.3.0/lib/php/extensions/no-debug-non-zts-20180731/
Installing PHP CLI binary:        /usr/local/php7.3.0/bin/
Installing PHP CLI man page:      /usr/local/php7.3.0/php/man/man1/
Installing PHP FPM binary:        /usr/local/php7.3.0/sbin/
Installing PHP FPM defconfig:     /usr/local/php7.3.0/etc/
Installing PHP FPM man page:      /usr/local/php7.3.0/php/man/man8/
Installing PHP FPM status page:   /usr/local/php7.3.0/php/php/fpm/
Installing phpdbg binary:         /usr/local/php7.3.0/bin/
Installing phpdbg man page:       /usr/local/php7.3.0/php/man/man1/
Installing PHP CGI binary:        /usr/local/php7.3.0/bin/
Installing PHP CGI man page:      /usr/local/php7.3.0/php/man/man1/
Installing build environment:     /usr/local/php7.3.0/lib/php/build/
Installing header files:          /usr/local/php7.3.0/include/php/
Installing helper programs:       /usr/local/php7.3.0/bin/
  program: phpize
  program: php-config
Installing man pages:             /usr/local/php7.3.0/php/man/man1/
  page: phpize.1
  page: php-config.1
/usr/local/src/php-src-php-7.3.0RC4/build/shtool install -c ext/phar/phar.phar /usr/local/php7.3.0/bin
ln -s -f phar.phar /usr/local/php7.3.0/bin/phar
Installing PDO headers:           /usr/local/php7.3.0/include/php/ext/pdo/


```
* php.ini 
* cp /usr/local/src/php-src-php-7.3.0RC4/php.ini-development /usr/local/php7.3.0/etc/
* cp /usr/local/src/php-src-php-7.3.0RC4/php.ini-production /usr/local/php7.3.0/etc/
* cd /usr/local/php7.3.0/etc
* mkdir php.d
* mv php.ini-development php.ini

* 服务化
* php-fpm.conf
* cp php-fpm.conf.default php-fpm.conf
* cd php-fpm.d
* cp www.conf.default www.conf
* 因为本地已经安装php5.6:9000, 7.2:9007 所以重新启动一个端口listen = 127.0.0.1:9008
* fpm服务化 strat/stop/restart
* cd /usr/local/src/php-src-php-7.3.0RC4/sapi/fpm/
* cp init.d.php-fpm /etc/init.d/php-fpm7.3.0
* chmod +x /etc/init.d/php-fpm7.3.0
* chkconfig --add php-fpm7.3.0
* chkconfig php-fpm7.3.0 on

* 如果没安装chkconfig:error:-bash: chkconfig: command not found
* 安装chkconfig https://github.com/jason-gao/docs/blob/master/linux/chkconfig.md
* /sbin/service php-fpm7.3.0 start启动fpm

* 发信号重启
    * /usr/local/php7.3.0/sbin/php-fpm
    * kill -USR2 `cat /usr/local/php7.3.0/var/run/php-fpm.pid`


* 添加个软链：ln -s /usr/local/php7.3.0/bin/php /usr/bin/php730
* 直接可以php730访问php
* php730 -m
* php730 -v
