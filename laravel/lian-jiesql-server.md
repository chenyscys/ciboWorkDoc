1.env 文件添加数据库配置，config/database.php 文件添加

```
'sqlsrv' => [
    'driver' => 'sqlsrv',
    'host' => env('SQLSVR_DB_HOST', 'localhost'),
    'port' => env('SQLSVR_DB_PORT', '1433'),
    'database' => env('SQLSVR_DB_DATABASE', 'forge'),
    'username' => env('SQLSVR_DB_USERNAME', 'forge'),
    'password' => env('SQLSVR_DB_PASSWORD', ''),
    'charset' => 'utf8',
    'prefix' => '',
]
```

2.web 服务器开启 pdo\_sqlsrv 扩展

> windows 环境

```
# 编辑 php.ini 文件，添加 php 版本对应的扩展
extension=php_sqlsrv_7_nts_x86.dll
extension=php_pdo_sqlsrv_7_nts_x86.dll
# 访问 https://www.microsoft.com/zh-CN/download/details.aspx?id=36434，下载安装 ODBC Driver
```

3.重启 web 服务器

4.模型文件

```
<?php

namespace App\Entities;

use Illuminate\Database\Eloquent\Model;

class ModelName extends Model
{
    /**
     * @var string
     */
    protected $connection = 'sqlsrv';

    /**
     * @var string
     */
    public $table = 'table_name';
}
```

> 参考链接：[https://phpartisan.cn/news/24.html](https://phpartisan.cn/news/24.html)



