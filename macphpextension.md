# php7.2 mysql 扩展
    * cd /usr/local/src/phpext
    * wget -c 'http://git.php.net/?p=pecl/database/mysql.git;a=snapshot;h=386776d22c226f3ac6f003dd31a823c77687cc44;sf=tgz' -O mysql.tar.gz
    * tar -zxvf mysql.tar.gz
    * cd mysql-386776d
    * /usr/local/opt/php@7.2/bin/phpize
    * ./configure --with-php-config=/usr/local/opt/php@7.2/bin/php-config --with-mysql=mysqlnd
    * make clean
    * make
    * make test
    * make install
    * Installing shared extensions:     /usr/local/Cellar/php@7.2/7.2.19/pecl/20170718/
    * cd /usr/local/Cellar/php@7.2/7.2.19/pecl/20170718/
    * vim /usr/local/etc/php/7.2/php.ini
    * extension=mysql.so
    * php -m