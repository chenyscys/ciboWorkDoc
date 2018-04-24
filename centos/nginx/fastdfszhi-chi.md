安装fastdfs module模块

cd /app/soft/nginx/conf

./configure --prefix=/app/soft/nginx --add-module=/app/fastdfs-nginx-module-master/src

make & make install

安装图片裁剪image\_filter

_http://blog.csdn.net/clevercode/article/details/52278482_

./configure --prefix=/app/soft/nginx --add-module=/app/fastdfs-nginx-module-master/src  --with-http\_image\_filter\_module

