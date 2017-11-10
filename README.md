### vue-cli 创建的项目，部署在 nginx 上的配置

```
server {
    listen 80;
    server_name www.xxx.com;
    charset utf-8;
    access_log xxx/host.access.log;
    location / {
        root xxx/dist;
        try_files $uri $uri/ /index.html;
    }
}

```
