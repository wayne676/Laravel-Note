```php
"autoload": {
        "classmap": [
            "database"
        ],
        "psr-4": {
            "App\\": "app/"
        },
         "files": [
             "app/Helper/Meta_tagsHelper.php",
             "app/Helper/ConstantsHelper.php"
         ]
    },
```
    composer里面file属性添加文件路径
    在对应的路径要新建文件
### "app/Helper/ConstantsHelper.php"：
    ```php
    defined('SUBCATEGORY') or define('SUBCATEGORY', array('Educational','Electronics','Fashion','Gaming','Garden','Hardware and Tools','Home','Music','Outdoors','Party Supplies','Sporting Goods','Transportation','Other'));
    ```
    使用时候直接SUBCATEGORY
