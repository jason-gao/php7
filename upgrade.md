* php5.6->[php7.2.1](php7.2.1.md)

* https://stackoverflow.com/questions/10687804/how-to-use-spl-autoload-as-autoload-goes-deprecated
* https://github.com/ezyang/htmlpurifier/pull/156/commits/7da6eb7e3cb709667f913466e5dd673df79427f8
* https://github.com/ezyang/htmlpurifier/issues/154
* https://github.com/ezyang/htmlpurifier/pull/156/files
* https://github.com/nette/http/commit/4667ae05dbf18e3820bfe1d70cbf0a04b83a828e
* http://zeyulee.com/php/2017/06/08/upgrade-php7/
* http://www.syyong.com/php/Php5-5-upgrade-to-php7-2.html


* E_DEPRECATED
* http://blog.insight.sensiolabs.com/2017/02/02/deprecations-php-7-2.html

*  __autoload() is deprecated, use spl_autoload_register() instead
    * 项目里用到https://github.com/ezyang/htmlpurifier这个库
    * 解决办法：https://github.com/ezyang/htmlpurifier/pull/156/commits/7da6eb7e3cb709667f913466e5dd673df79427f8

* The each() function is deprecated. 
    This message will be suppressed on further calls
    * composer里加载了这个库：nette/http 
    * 解决办法：https://github.com/nette/http/blob/master/src/Http/RequestFactory.php
    * 使用foreach代替each
    * http://php.net/manual/zh/function.each.php

* Function create_function() is deprecated
    * https://github.com/luofei614/SocketLog/issues/42
    * https://wordpress.org/support/topic/v2-0-3-function-create_function-is-deprecated-in-php-7-2/
    * resolve:用匿名函数代替
    * http://php.net/manual/en/functions.anonymous.php
    * https://stackoverflow.com/questions/48161526/php-7-2-function-create-function-is-deprecated
    * http://blog.insight.sensiolabs.com/2017/02/02/deprecations-php-7-2.html
    * https://github.com/jason-gao/SocketLog/commit/c175c51f5bd034674c30368e4fd61851a2d0ac70

* idn_to_ascii
  * https://www.php.net/manual/zh/function.idn-to-ascii.php
  * Deprecated: idn_to_utf8(): INTL_IDNA_VARIANT_2003 is deprecated
  * solve:
  * https://github.com/egulias/EmailValidator/blob/master/EmailValidator/Validation/DNSCheckValidation.php
  * $res1 = idn_to_ascii($domain, IDNA_DEFAULT, INTL_IDNA_VARIANT_UTS46, $idna_info);
    
* 项目中用到memcache扩展全部改为memcached
    * php7.2官方没有相应的memcache扩展，建议直接安装memcached扩展
    * 扩展安装参照 extension.md
        
* E_ERROR
 * 如果有必传参数，调用时候没传,php5.6不会报错，php7.2会报fatal error
 * Uncaught ArgumentCountError: Too few arguments to function xx::yy(), 
  2 passed in xx.php on line 948 and exactly 3 expected in xxx.php:1304
    
* php7移除了mysql扩展
    * 为了兼容性需要安装mysql扩展
    * [mysql扩展](extention.md#mysqlextension)
    
* [] operator not supported for strings
    * https://stackoverflow.com/questions/5879675/problem-with-fatal-error-operator-not-supported-for-strings-in
    ```
    $foo = 'foo';
    $foo[] = 'bar'; // ERROR!
    ```
        