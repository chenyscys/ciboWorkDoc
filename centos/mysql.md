mysql容器

docker run --name db\_11\_01  -v /data/mysql/data:/var/lib/mysql -v /home/config/mysql:/etc/mysql/conf.d  -p 3316:3306  -e MYSQL\_ROOT\_PASSWORD=cibo8112. -d --restart=always mysql

