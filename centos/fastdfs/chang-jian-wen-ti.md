* ERROR - file: tracker\_proto.c, line: 48, server: 192.168.3.29:22122, response status 2 != 0
* Transport endpoint is not connected

关闭storage

重启tracker、storage

/usr/bin/fdfs\_trackerd /etc/fdfs/tracker.conf restart

/usr/bin/fdfs\_storaged /etc/fdfs/storage.conf restart

