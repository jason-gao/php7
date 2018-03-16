* 隐藏PHP 被安装在服务器上的标识，隐藏X-Powered-By:PHP/7.2.1-dev，建议生产环境隐藏
    * http://php.net/manual/zh/ini.core.php#ini.expose-php
    * vim php.ini -> expose_php = Off 关闭
    * 重启php-fpm后生效
    