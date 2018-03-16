
# memcache扩展 -官方已经不维护这个扩展了，建议使用memcached扩展
* 第三方维护：https://github.com/websupport-sk/pecl-memcache

```
wget -c https://github.com/websupport-sk/pecl-memcache/archive/NON_BLOCKING_IO_php7.zip
unzip NON_BLOCKING_IO_php7.zip
cd pecl-memcache-NON_BLOCKING_IO_php7/
/usr/local/php7.2.1/bin/phpize
./configure --with-php-config=/usr/local/php7.2.1/bin/php-config
make -j 2
make install

```
* Installing shared extensions:     /usr/local/php7.2.1/lib/php/extensions/no-debug-non-zts-20170718/
* vim /usr/local/php7.2.1/etc/php.ini
* extension=memcache.so
* service php-fpm7.2.1 restart 重启php-fpm，不然对web网站不起作用


# 编译memcached扩展
* https://github.com/php-memcached-dev/php-memcached
* https://github.com/php-memcached-dev/php-memcached/archive/v3.0.4.tar.gz

* 依赖libmemcached
* https://launchpad.net/libmemcached/+download
* https://launchpad.net/libmemcached/1.0/1.0.18/+download/libmemcached-1.0.18.tar.gz

* 安装libmemcached

```
wget -c https://launchpad.net/libmemcached/1.0/1.0.18/+download/libmemcached-1.0.18.tar.gz
tar -zxvf libmemcached-1.0.18.tar.gz
cd libmemcached-1.0.18
./configure --prefix=/usr/local/libmemcached --enable-sasl
make -j 5
make install
 
```

* sasl提供用户名与密码验证
* http://blog.csdn.net/chaozhi_guo/article/details/46713695

```
wget -c https://github.com/php-memcached-dev/php-memcached/archive/v3.0.4.tar.gz -O memcachedv3.0.4.tar.gz
tar -zxvf memcachedv3.0.4.tar.gz
cd php-memcached-3.0.4
/usr/local/php7.2.1/bin/phpize
./configure --with-libmemcached-dir=/usr/local/libmemcached/  --with-php-config=/usr/local/php7.2.1/bin/php-config --enable-memcached-sasl
make -j 2
make install

```
* Installing shared extensions:     /usr/local/php7.2.1/lib/php/extensions/no-debug-non-zts-20170718/
* vim /usr/local/php7.2.1/etc/php.ini
* extension=memcached.so
* service php-fpm7.2.1 restart 重启php-fpm，不然对web网站不起作用

 
# redis扩展安装
* https://github.com/phpredis/phpredis
* https://pecl.php.net/package/redis

```
cd /usr/local/src/php7ext
wget -c https://github.com/phpredis/phpredis/archive/3.1.6.tar.gz -O redis.3.1.6.tar.gz
tar -zxvf redis.3.1.6.tar.gz
cd phpredis-3.1.6/
/usr/local/php7.2.1/bin/phpize
./configure --with-php-config=/usr/local/php7.2.1/bin/php-config
make -j 2
make install

```
* Installing shared extensions:     /usr/local/php7.2.1/lib/php/extensions/no-debug-non-zts-20170718/
* vim /usr/local/php7.2.1/etc/php.ini
* extension=redis.so
* service php-fpm7.2.1 restart 重启php-fpm，不然对web网站不起作用

# bcmath扩展 php源码包里有

```
cd /usr/local/src/php-src-php-7.2.1/ext
cd bcmath
/usr/local/php7.2.1/bin/phpize
./configure --with-php-config=/usr/local/php7.2.1/bin/php-config
make -j 2
make install
cd /usr/local/php7.2.1/lib/php/extensions/no-debug-non-zts-20170718/
vim /usr/local/php7.2.1/etc/php.ini
extension=bcmath.so
service php-fpm7.2.1 restart 重启php-fpm，不然对web网站不起作用

```
* 如果编译时候加了--enable-bcmath，则这里不需要再编译
* 否则会报PHP Startup: Invalid library (maybe not a PHP library) 'bcmath.so' in <b>Unknown</b> on line
* php.ini里的extension=bcmath.so去掉即可，因为已经默认加载了


# amqp扩展 操作rabitmq
* https://github.com/pdezwart/php-amqp/releases
* https://github.com/alanxz/rabbitmq-c/releases

* librabbitmq not found
* 先安装 librabbitmq
* yum install librabbitmq-devel

```
cd /usr/local/src/php7ext
wget -c https://github.com/pdezwart/php-amqp/archive/v1.9.3.tar.gz
tar -zxvf v1.9.3.tar.gz
cd php-amqp-1.9.3
/usr/local/php7.2.1/bin/phpize
./configure --with-php-config=/usr/local/php7.2.1/bin/php-config --with-amqp 
make -j 2
make install

```

* 加到php.ini里
```
extension=memcached.so
extension=memcache.so
extension=redis.so
extension=bcmath.so
extension=amqp.so

```
  