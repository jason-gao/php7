# notice
    * 如果需要将 » Xdebug 扩展和 OPcache 一起使用，必须在 Xdebug 扩展之前加载 OPcache 扩展。

# 清理opcache
 - http://gordalina.github.io/cachetool/
 - https://github.com/PeeHaa/OpCacheGUI
    
    * cachetool
        * $ curl -sO http://gordalina.github.io/cachetool/downloads/cachetool.phar
          $ chmod +x cachetool.phar
        * php721 cachetool.phar opcache:status --fcgi=127.0.0.1:9007  
        * php721 cachetool.phar opcache:reset --fcgi=127.0.0.1:9007  
        * php721 cachetool.phar opcache:configuration --fcgi=127.0.0.1:9007  
    
