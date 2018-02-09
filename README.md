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

* 添加个软链：ln -s /usr/local/php7.2.1/bin/php /usr/bin/php721
* 直接可以php721访问php
* php721 -m
* php721 -v


## benchmark
* hello world
* php5.6 vs php7.2.1
* 127.0.0.1 php56.vm
* 127.0.0.1 php721.vm

## nginx conf
* php5.6.conf

```
server {
    listen       80;
    server_name  php56.vm;
    access_log  /var/log/nginx/php56.vm.access.log;
    error_log   /var/log/nginx/php56.vm.error.log;
    root /usr/local/src/phpCode/;
    index index.php index.html index.htm;


    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9007;
        fastcgi_index  index.php;
        include fastcgi.conf;
        include fastcgi_params;
    }

}

```
* php php7.2.1.conf
```
server {
    listen       80;
    server_name  php721.vm;
    access_log  /var/log/nginx/php721.vm.access.log;
    error_log   /var/log/nginx/php721.vm.error.log;
    root /usr/local/src/phpCode/;
    index index.php index.html index.htm;


    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9007;
        fastcgi_index  index.php;
        include fastcgi.conf;
        include fastcgi_params;
    }

}

```

* ab -c10 -n50000 http://php56.vm/
```
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking php56.vm (be patient)
Completed 5000 requests
Completed 10000 requests
Completed 15000 requests
Completed 20000 requests
Completed 25000 requests
Completed 30000 requests
Completed 35000 requests
Completed 40000 requests
Completed 45000 requests
Completed 50000 requests
Finished 50000 requests


Server Software:        nginx/1.8.1
Server Hostname:        php56.vm
Server Port:            80

Document Path:          /
Document Length:        11 bytes

Concurrency Level:      10
Time taken for tests:   10.128 seconds
Complete requests:      50000
Failed requests:        0
Write errors:           0
Total transferred:      8800000 bytes
HTML transferred:       550000 bytes
Requests per second:    4936.81 [#/sec] (mean)
Time per request:       2.026 [ms] (mean)
Time per request:       0.203 [ms] (mean, across all concurrent requests)
Transfer rate:          848.51 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       5
Processing:     0    2   0.9      2      28
Waiting:        0    2   0.9      2      28
Total:          1    2   0.9      2      28

Percentage of the requests served within a certain time (ms)
  50%      2
  66%      2
  75%      2
  80%      2
  90%      3
  95%      3
  98%      4
  99%      5
 100%     28 (longest request)
```
* ab -c10 -n50000 http://php721.vm/
```
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking php721.vm (be patient)
Completed 5000 requests
Completed 10000 requests
Completed 15000 requests
Completed 20000 requests
Completed 25000 requests
Completed 30000 requests
Completed 35000 requests
Completed 40000 requests
Completed 45000 requests
Completed 50000 requests
Finished 50000 requests


Server Software:        nginx/1.8.1
Server Hostname:        php721.vm
Server Port:            80

Document Path:          /
Document Length:        11 bytes

Concurrency Level:      10
Time taken for tests:   10.055 seconds
Complete requests:      50000
Failed requests:        0
Write errors:           0
Total transferred:      8800000 bytes
HTML transferred:       550000 bytes
Requests per second:    4972.83 [#/sec] (mean)
Time per request:       2.011 [ms] (mean)
Time per request:       0.201 [ms] (mean, across all concurrent requests)
Transfer rate:          854.70 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0      10
Processing:     0    2   1.3      2      60
Waiting:        0    2   1.3      2      60
Total:          1    2   1.3      2      60

Percentage of the requests served within a certain time (ms)
  50%      2
  66%      2
  75%      2
  80%      2
  90%      3
  95%      3
  98%      4
  99%      5
 100%     60 (longest request)
 
```
