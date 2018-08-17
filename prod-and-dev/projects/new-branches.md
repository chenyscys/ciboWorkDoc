#### 一、创建分支![](/assets/新建分支.png)![](/assets/分支命名.png)

#### 二、取出分支

![](/assets/取出分支.png)

checkout分支，并进行相关文件修改配置、删除

![](/assets/配置文件.png)

#### 三、部署到服务器，并配置

svn co svn://192.168.3.29/svn/summer\_system/oa/branches/{分支名} /home/www/oa/branches/{分支名}

安装laravel扩展

cd /home/www/oa/branches/{分支名}

composer install  或 composer update

设置目录权限

chmod -R 777 public storage

清理缓存

php artisan config:cache  --env=production

配置socket地址

![](/assets/socket.png)

![](/assets/laravel-echo-server.png)

#### 四、nginx解析到项目

cd /app/soft/nginx/conf/conf.d/

![](/assets/nginx.png)

修改项目文件，eg

vi 8012.cibohome.conf

![](/assets/8012.png)

修改完毕后，重启nginx即可

#### 五、正常访问



