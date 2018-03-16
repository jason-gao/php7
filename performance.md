* 提升性能
* http://www.laruence.com/2015/12/04/3086.html
* https://github.com/PeeHaa/OpCacheGUI opcache gui
* https://github.com/rlerdorf/opcache-status


* 启用opcache
    * php.ini加入
    ```
    ;opcache
    zend_extension=opcache.so
    opcache.enable=1
    opcache.enable_cli=1
    ```
    * 添加完后 php -m 查看扩展有Zend OPcache代表启用成功
    * 如果是web项目，需要重启php-fpm

    * [HugePage]
    * /sbin/sysctl vm.nr_hugepages=512
    * cat /proc/meminfo  | grep Huge
    ```
    ;opcache
    zend_extension=opcache.so
    opcache.enable=1
    opcache.enable_cli=1
    opcache.huge_code_pages=1
    ```