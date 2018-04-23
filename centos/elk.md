## 以下是3.29服务器上的配置：

## **启动命令**

elasticsearch启动：

```
su - elasticsearch <<EOF
/mnt/xvdb1/app/software/elasticsearch/bin/elasticsearch &
exit
EOF
```

elasticsearch-head启动：

```
cd /mnt/xvdb1/app/software/elasticsearch-head
npm run start &
```

logstash启动：

```
/mnt/xvdb1/app/software/logstash/bin/logstash -f /mnt/xvdb1/app/software/logstash/config/logstash_redis_out.conf &
```

filebeat启动：

```
/mnt/xvdb1/app/software/filebeat/filebeat -e -c /mnt/xvdb1/app/software/filebeat/filebeat_redis_in.yml -d "Publish" &
```

kibana 启动：

```
/mnt/xvdb1/app/software/kibana/bin/kibana &
```

## 配置文件

elasticsearch配置文件：

/mnt/xvdb1/app/software/elasticsearch/config/elasticsearch.yml

```
# 除了第一行，其他不要修改
cluster.name: elk-cibo
network.host: 0.0.0.0
http.port: 9200
transport.host: localhost
transport.tcp.port: 9300
http.cors.enabled: true
http.cors.allow-origin: "*"
```

logstash配置文件：

/mnt/xvdb1/app/software/logstash/config/logstash\_redis\_out.conf

```
  # nginx的错误日志，使用默认的log即可，本正则已匹配好，并且切割。
  if [service_type] == "nginx_error"{
    grok {
      match => { "message" => "(?<time>%{YEAR}[./-]%{MONTHNUM}[./-]%{MONTHDAY}[- ]%{TIME}) %{NOTSPACE:error_type} (?<content>.*\s+)"}
    }
  }

  # nginx的访问日志，使用默认的log即可，本正则已匹配好，并且切割。
  if [service_type] == "nginx_access"{
    grok {
      match => {"message" => "%{NOTSPACE:clientip} - - \[%{TIMESTAMP_ISO8601:timestamp}\] \"(?:%{WORD:verb} %{NOTSPACE:request}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:rawrequest})\" %{NUMBER:response} %{NUMBER:bytes} %{QS:referrer} %{QS:agent}"}
    }
  }

  #这句是过滤静态资源用的
  if ([message] =~ "\.(jpg|jpeg|css|js|mp3|png|ico)") {
    drop {}
  }



  output {

    # 索引分类用，按照类名-日期进行分类
    if [service_type] == "laravel"{
        elasticsearch {
           hosts => ["192.168.3.29:9200"]
           index => "laravel-%{+YYYY.MM.dd}"
        }
    }

    if [service_type] == "easywechat"{
        elasticsearch {
           hosts => ["192.168.3.29:9200"]
           index => "easywechat-%{+YYYY.MM.dd}"
        }
    }
```

filebeat配置文件：

/mnt/xvdb1/app/software/filebeat/filebeat\_redis\_in.yml

```
filebeat.prospectors:

# 日志多行分行，日志类型：laravel
- type: log
  paths:
    - /mnt/xvdb1/www/composer/ciboapp/storage/logs/laravel*
  fields:
    service_type: laravel
  fields_under_root: true
  multiline.pattern: '^\[[0-9]{4}-[0-9]{2}-[0-9]{2}'
  multiline.negate: true
  multiline.match: after
  multiline.timeout: 2s

# 日志多行分行，日志类型：easywechat
- type: log
  paths:
    - /mnt/xvdb1/www/composer/ciboapp/storage/logs/easywechat*
  fields:
    service_type: easywechat
  fields_under_root: true
  multiline.pattern: '^\[[0-9]{4}-[0-9]{2}-[0-9]{2}'
  multiline.negate: true
  multiline.match: after
  multiline.timeout: 2s

# 日志类型：nginx_access
- type: log
  paths:
    - /app/soft/nginx/logs/access.log
  fields:
    service_type: nginx_access
  fields_under_root: true
```



