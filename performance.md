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
        * /sbin/sysctl -w vm.nr_hugepages=512
        * cat /proc/meminfo  | grep Huge
    * 不设置这个会导致waring  Zend OPcache huge_code_pages: mmap(HUGETLB) failed: Cannot allocate memory (12) in Unknown on line 0    
    ```
    ;opcache
    zend_extension=opcache.so
    opcache.enable=1
    opcache.enable_cli=1
    opcache.huge_code_pages=1
    ```