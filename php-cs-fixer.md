* php-cs-fixer 代码风格管理，可以放到git钩子里，提交前自动格式化代码

    * https://github.com/FriendsOfPHP/PHP-CS-Fixer/blob/2.10/composer.json
    * php-cs-fixer
        * 安装了多版本php执行php-cs-fixer
        * php721 vendor/friendsofphp/php-cs-fixer/php-cs-fixer fix [--dry-run -vvv]
        * 加载.php_cs.dist这个配置文件
    
     ```
        "require-dev": {
            "friendsofphp/php-cs-fixer": "^2.10|^2.2"
        }
    ```   