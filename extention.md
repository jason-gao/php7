
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

# 安装xdebug扩展
    * https://xdebug.org/download.php
    - A list of all settings:  http://xdebug.org/docs-settings.php     
    - A list of all functions: http://xdebug.org/docs-functions.php    
    - Profiling instructions:  http://xdebug.org/docs-profiling2.php   
    - Remote debugging:        http://xdebug.org/docs-debugger.php 

* cd /usr/local/src/php7ext
* wget -c https://xdebug.org/files/xdebug-2.6.0.tgz
* tar -zxvf xdebug-2.6.0.tgz
* cd xdebug-2.6.0
* /usr/local/php7.2.1/bin/phpize
* ./configure --enable-xdebug --with-php-config=/usr/local/php7.2.1/bin/php-config
* make -j 2
* make test
* make install
* vim /usr/local/php7.2.1/etc/php.ini
```

[Xdebug]  
zend_extension="/usr/local/php7.2.1/lib/php/extensions/no-debug-non-zts-20170718/xdebug.so"  
xdebug.profiler_enable=on   
xdebug.trace_output_dir="/usr/local/php7.2.1/xdebug/"  
xdebug.profiler_output_dir="/usr/local/php7.2.1/xdebug/"  
xdebug.remote_enable=on             
xdebug.remote_handler=dbgp            
xdebug.remote_host=192.168.5.118  
xdebug.remote_port=9999
 
```

# 安装swoole
    * https://github.com/swoole/swoole-src/archive/v1.10.2.tar.gz
    * https://github.com/swoole/swoole-src/archive/v2.1.1.tar.gz  (wiki)[https://wiki.swoole.com/]
    * 2.0 支持协程

## swoole 1.10.2
* cd /usr/local/src/php7ext
* wget -c https://github.com/swoole/swoole-src/archive/v1.10.2.tar.gz -O swoole-v1.10.2.tar.gz
* tar -zxvf swoole-v1.10.2.tar.gz
* cd swoole-src-1.10.2
* /usr/local/php7.2.1/bin/phpize
* ./configure --with-php-config=/usr/local/php7.2.1/bin/php-config
* make
* make test
* make install
* vim /usr/local/php7.2.1/etc/php.ini     

## swoole 2.1.1
* cd /usr/local/src/php7ext
* wget -c https://github.com/swoole/swoole-src/archive/v2.1.1.tar.gz -O swoole-v2.1.1.tar.gz
* tar -zxvf swoole-v2.1.1.tar.gz
* cd swoole-src-2.1.1
* /usr/local/php7.2.1/bin/phpize --clean
* /usr/local/php7.2.1/bin/phpize
* ./configure --with-php-config=/usr/local/php7.2.1/bin/php-config --enable-async-redis
* make -j 2
* make test
* make install
* vim /usr/local/php7.2.1/etc/php.ini
   
   * --enable-async-redis question: 
    * https://www.imooc.com/wenda/detail/387830
    * https://wiki.swoole.com/wiki/page/p-redis.html
    * --enable-async-redis 依赖hiredis 
        * error:‘swRedisClient’ has no member named ‘context’
        * https://github.com/redis/hiredis/releases
        * https://github.com/redis/hiredis/archive/v0.13.3.tar.gz
        * cd /usr/local/src/php7ext
        * wget -c https://github.com/redis/hiredis/archive/v0.13.3.tar.gz -O hiredis-v0.13.3.tar.gz
        * tar -zxvf hiredis-v0.13.3.tar.gz
        * cd hiredis-0.13.3/
        * make
        * make install
            ```bash
              mkdir -p /usr/local/include/hiredis /usr/local/lib
              cp -a hiredis.h async.h read.h sds.h adapters /usr/local/include/hiredis
              cp -a libhiredis.so /usr/local/lib/libhiredis.so.0.13
              cd /usr/local/lib && ln -sf libhiredis.so.0.13 libhiredis.so
              cp -a libhiredis.a /usr/local/lib
              mkdir -p /usr/local/lib/pkgconfig
              cp -a hiredis.pc /usr/local/lib/pkgconfig
            ```
        * hiredis默认是装在/usr/local/lib下的
        * cd /etc/ld.so.conf.d
        * echo "/usr/local/lib" >> hiredis.conf
        * ldconfig
        
        * 或者
            * vi ~/.bash_profile
            * export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
            * source ~/.bash_profile
            * ldconfig

* 加到php.ini里 /usr/local/php7.2.1/etc/php.ini
    * .so文件路径 /usr/local/php7.2.1/lib/php/extensions/no-debug-non-zts-20170718/

    
## swoole 4.2.9
* cd /usr/local/src/php7ext
* wget -c https://github.com/swoole/swoole-src/archive/v4.2.9.tar.gz -O swoole-v4.2.9.tar.gz
* tar -zxvf swoole-v4.2.9.tar.gz
* cd swoole-src-4.2.9
* /usr/local/php7.2.1/bin/phpize --clean
* /usr/local/php7.2.1/bin/phpize
* ./configure --with-php-config=/usr/local/php7.2.1/bin/php-config
* make clean
* make ->gcc error
* make test
* make install
* vim /usr/local/php7.2.1/etc/php.ini 
    ### error
    * GCC 4.8 or later required
    * https://gist.github.com/stephenturner/e3bc5cfacc2dc67eca8b
    * https://github.com/swoole/swoole-src/issues/2064#event-1925303808
    * https://forum.phalconphp.com/discussion/17595/problem-with-compiled-phalcon-with-php-721
    
    ```
        $ cat /etc/centos-release
        $ sudo yum install centos-release-scl
        $ sudo yum install devtoolset-7-toolchain
        $ scl enable devtoolset-7 bash
        $ source /opt/rh/devtoolset-7/enable
        $ gcc --version
        
        ...
    ```
 
## swoole 4.3.1
* cd /usr/local/src/php7ext
* wget -c https://github.com/swoole/swoole-src/archive/v4.3.1.tar.gz -O swoole-v4.3.1.tar.gz
* tar -zxvf swoole-v4.3.1.tar.gz
* cd swoole-src-4.3.1
* /usr/local/php7.2.1/bin/phpize --clean
* /usr/local/php7.2.1/bin/phpize
* ./configure --with-php-config=/usr/local/php7.2.1/bin/php-config CFLAGS=-fPIC
* make clean
* make ->gcc error
* make test
* make install
* - /usr/local/php7.2.1/lib/php/extensions/no-debug-non-zts-20170718/
* vim /usr/local/php7.2.1/etc/php.ini 
    ### error
    * GCC 4.8 or later required
    * https://gist.github.com/stephenturner/e3bc5cfacc2dc67eca8b
    * https://github.com/swoole/swoole-src/issues/2064#event-1925303808
    * https://forum.phalconphp.com/discussion/17595/problem-with-compiled-phalcon-with-php-721
    * https://docs.lvrui.io/2016/12/12/CentOS6-x%E4%B8%8B%E7%9A%84gcc%E5%8D%87%E7%BA%A7/
    
    ```
        $ cat /etc/centos-release
        $ sudo yum install centos-release-scl
        $ sudo yum install devtoolset-7-toolchain
        $ scl enable devtoolset-7 bash
        $ source /opt/rh/devtoolset-7/enable
        $ gcc --version
        
        ...
    ```
   ### error:
    /opt/rh/devtoolset-7/root/usr/libexec/gcc/x86_64-redhat-linux/7/ld: src/core/.libs/error.o: relocation R_X86_64_32 against `.rodata.str1.1' can not be used when making a shared object; recompile with -fPIC
    
    system:
    CentOS release 6.8 (Final) x86_64
    PHP 7.2.1-dev
    swoole 4.3.1
    ->
    ./configure --with-php-config=/usr/local/php7.2.1/bin/php-config CFLAGS=-fPIC
    
    
    
## <span id="mysqlextension">mysql</span>
  * php7移除了mysql扩展
  * http://git.php.net/?p=pecl/database/mysql.git;a=summary
  * cd /usr/local/src/php7ext
  * wget -c 'http://git.php.net/?p=pecl/database/mysql.git;a=snapshot;h=386776d22c226f3ac6f003dd31a823c77687cc44;sf=tgz' -O mysql.tar.gz
  * tar -zxvf mysql.tar.gz
  * cd mysql-386776d
  * /usr/local/php7.2.1/bin/phpize --clean
  * /usr/local/php7.2.1/bin/phpize
  * ./configure --with-php-config=/usr/local/php7.2.1/bin/php-config --with-mysql=mysqlnd
  * make clean
  * make
  * make test
  * make install
  * cd /usr/local/php7.2.1/lib/php/extensions/no-debug-non-zts-20170718/
  * vim /usr/local/php7.2.1/etc/php.ini 
  * extension=mysql.so
  * php721 -m
  
  
## xhprof
- 官方0.9.4编译不通过
```text
/tmp/pear/install/xhprof/extension/xhprof.c:1991: error: ‘zval’ has no member named ‘type’
make: *** [xhprof.lo] Error 1
ERROR: `make' failed
```
- https://github.com/longxinH/xhprof/ 第三方

- cd /data/soft
- git clone https://github.com/longxinH/xhprof.git
- cd xhprof/extension/
- /usr/local/php7.2.1/bin/phpize
- ./configure --with-php-config=/usr/local/php7.2.1/bin/php-config
- make && sudo make install
- vim /usr/local/php7.2.1/etc/php.ini
- [xhprof]
  extension = xhprof.so
  xhprof.output_dir = /tmp/xhprof721
- kill -USR2 4416  重启php-fpm
- php721 -m

- error
- https://segmentfault.com/a/1190000003509917
failed to execute cmd: " dot -Tpng". stderr: `sh: dot: command not found '
- linux-centos
sudo yum install graphviz
- mac 
brew install graphviz

将分析结果放到 xhprof.output_dir
- 先创建目录 mkdir /tmp/xhprof721 && cd /tmp/xhprof721

```php

$xhprofData = xhprof_disable();
require '/vagrant/xhprof/xhprof_lib/utils/xhprof_lib.php';
require '/vagrant/xhprof/xhprof_lib/utils/xhprof_runs.php';

$xhprofRuns = new XHProfRuns_Default();
$runId = $xhprofRuns->save_run($xhprofData, 'xhprof_test');

echo 'http://localhost/xhprof/xhprof_html/index.php?run=' . $runId . '&source=xhprof_test';

```

  
    
```
extension=memcached.so
extension=memcache.so
extension=redis.so
extension=bcmath.so
extension=amqp.so
extension=swoole.so
extension=mysql.so
extension = xhprof.so

```
  