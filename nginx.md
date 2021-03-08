# nginx LB

## fedora 
```bash
yum -y install nginx nginx-mod-stream
```
add section in nginx.conf

``` /etc/nginx/nginx.conf
stream {
    log_format  main  '$remote_addr - [$time_local] ';

    access_log  /var/log/nginx/stream.log  main;
    include /etc/nginx/conf.d/*.stream;
}
```

add tcp stream config 

``` mstsc.stream
upstream hostname_mstsc {
  server 172.20.2.101:3389;
  server 172.20.2.102:3389;
}

server {
  listen 3389;
  proxy_pass hostname_mstsc;
}

```



# Troublshooting
nginx troubleshooting too many open files

## get pid
ps aux | grep nginx

## see limits
cat /proc/pid/limits

## see open files
ls -l /proc/pid/fd/*
