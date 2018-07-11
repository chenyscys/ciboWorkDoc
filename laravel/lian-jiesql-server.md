> env 文件添加数据库配置，config/database.php 文件添加

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

> web服务器开启 pdo\_sqlsrv 扩展，php.ini文件，添加

```
extension=php_pdo_sqlsrv_7_nts_x86.dll
```



