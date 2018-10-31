# centos 安装php7.2.1

* https://github.com/php/php-src
* https://drive.google.com/file/d/0B3UKOMH_4lgBUTdjUGxIZ3l1Ukk/view
* http://php.net/manual/zh/migration70.php
* https://segmentfault.com/a/1190000004123048
* https://segmentfault.com/a/1190000009909817
* https://www.cnblogs.com/apexchu/p/4193117.html
* https://github.com/wuxu92/PHP7-Reference-cn
* https://mp.weixin.qq.com/s?__biz=MzIwNDExMjIzNA==&mid=401084310&idx=1&sn=82e16e3096862fc2ca460072bd7350d7&scene=23&srcid=1204VvYIHoePMaPt2VWSNdsh#rd

# error
* 源码下载不全，信息丢失
* gzip: stdin: unexpected end of file
* http://blog.csdn.net/qq_29350001/article/details/51954801
## -----------------------------------------------------------
* autoconf 版本过低
```
buildconf: checking installation...
buildconf: autoconf version 2.63 found.
           You need autoconf version 2.64 or newer installed
           to build PHP from Git.
make: *** [buildmk.stamp] Error 1
```
* upgrade autoconf 2.63->2.64
* http://blog.csdn.net/a657941877/article/details/17173193
* ftp://ftp.gnu.org/gnu/autoconf/
```
* 查看当前版本
    * rpm -qf /usr/bin/autoconf 
* 卸载当前版本
    * rpm -e --nodeps autoconf-2.63
* cd /usr/local/src    
* wget -c http://ftp.gnu.org/gnu/autoconf/autoconf-2.69.tar.gz
    * tar -zxvf autoconf-2.69.tar.gz
    * cd autoconf-2.69
    * ./configure --prefix=/usr
    * make && make install
```
## ------------------------------------------------------------


* yum -y install libxml2 libxml2-devel openssl openssl-devel curl-devel libjpeg-devel libpng-devel freetype-devel libmcrypt-devel

* wget -c https://github.com/php/php-src/archive/php-7.2.1.tar.gz
* cd /usr/local/src && tar -zxvf php-7.2.1.tar.gz
* cd /usr/local/src/php-src-php-7.2.1
* ./buildconf，如提示autoconf版本过低，参考上面error进行升级，如正确会生成confiure文件
* 
```

./configure --prefix=/usr/local/php7.2.1 \
--with-config-file-path=/usr/local/php7.2.1/etc \
--with-config-file-scan-dir=/usr/local/php7.2.1/etc/php.d \
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

```
* make -j 2
* make install
```
Installing shared extensions:     /usr/local/php7.2.1/lib/php/extensions/no-debug-non-zts-20170718/
Installing PHP CLI binary:        /usr/local/php7.2.1/bin/
Installing PHP CLI man page:      /usr/local/php7.2.1/php/man/man1/
Installing PHP FPM binary:        /usr/local/php7.2.1/sbin/
Installing PHP FPM defconfig:     /usr/local/php7.2.1/etc/
Installing PHP FPM man page:      /usr/local/php7.2.1/php/man/man8/
Installing PHP FPM status page:   /usr/local/php7.2.1/php/php/fpm/
Installing phpdbg binary:         /usr/local/php7.2.1/bin/
Installing phpdbg man page:       /usr/local/php7.2.1/php/man/man1/
Installing PHP CGI binary:        /usr/local/php7.2.1/bin/
Installing PHP CGI man page:      /usr/local/php7.2.1/php/man/man1/
Installing build environment:     /usr/local/php7.2.1/lib/php/build/
Installing header files:          /usr/local/php7.2.1/include/php/
Installing helper programs:       /usr/local/php7.2.1/bin/
  program: phpize
  program: php-config
Installing man pages:             /usr/local/php7.2.1/php/man/man1/
  page: phpize.1
  page: php-config.1
/usr/local/src/php-src-php-7.2.1/build/shtool install -c ext/phar/phar.phar /usr/local/php7.2.1/bin
ln -s -f phar.phar /usr/local/php7.2.1/bin/phar
Installing PDO headers:           /usr/local/php7.2.1/include/php/ext/pdo/

```
* php.ini 
* cp /usr/local/src/php-src-php-7.2.1/php.ini-development /usr/local/php7.2.1/etc/
* cp /usr/local/src/php-src-php-7.2.1/php.ini-production /usr/local/php7.2.1/etc/
* cd /usr/local/php7.2.1/etc
* mkdir php.d
* mv php.ini-development php.ini

* 服务化
* php-fpm.conf
* cp php-fpm.conf.default php-fpm.conf
* cd php-fpm.d
* cp www.conf.default www.conf
* 因为本地已经安装php5.6,所以重新启动一个端口listen = 127.0.0.1:9007
* fpm服务化 strat/stop/restart
* cd /usr/local/src/php-src-php-7.2.1/sapi/fpm/
* cp init.d.php-fpm /etc/init.d/php-fpm7.2.1
* chmod +x /etc/init.d/php-fpm7.2.1
* chkconfig --add php-fpm7.2.1
* chkconfig php-fpm7.2.1 on

* 如果没安装chkconfig:error:-bash: chkconfig: command not found
* 安装chkconfig https://github.com/jason-gao/docs/blob/master/linux/chkconfig.md
* /sbin/service php-fpm7.2.1 start启动fpm

* 发信号重启
    * /usr/local/php7.2.1/sbin/php-fpm
    * kill -USR2 `cat /usr/local/php7.2.1/var/run/php-fpm.pid`


* 添加个软链：ln -s /usr/local/php7.2.1/bin/php /usr/bin/php721
* 直接可以php721访问php
* php721 -m
* php721 -v
