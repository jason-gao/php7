* php5.6->php7.2.1

* https://stackoverflow.com/questions/10687804/how-to-use-spl-autoload-as-autoload-goes-deprecated
* https://github.com/ezyang/htmlpurifier/pull/156/commits/7da6eb7e3cb709667f913466e5dd673df79427f8
* https://github.com/ezyang/htmlpurifier/issues/154
* https://github.com/ezyang/htmlpurifier/pull/156/files
* https://github.com/nette/http/commit/4667ae05dbf18e3820bfe1d70cbf0a04b83a828e

* E_DEPRECATED
*  __autoload() is deprecated, use spl_autoload_register() instead
    * 项目里用到https://github.com/ezyang/htmlpurifier这个库
    * 解决办法：https://github.com/ezyang/htmlpurifier/pull/156/commits/7da6eb7e3cb709667f913466e5dd673df79427f8

* The each() function is deprecated. 
    This message will be suppressed on further calls
    * composer里加载了这个库：nette/http 
    * 解决办法：https://github.com/nette/http/commit/4667ae05dbf18e3820bfe1d70cbf0a04b83a828e
    * http://php.net/manual/zh/function.each.php
    
* 项目中用到memcache扩展全部改为memcached
    * 扩展安装参照 extension.md

    
    
        