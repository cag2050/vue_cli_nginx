### vue-cli 创建的项目，部署在 nginx 上的配置

```
server {
    listen 80;
    server_name query.miaopai.com;
    charset utf-8;
    location / {
        try_files $uri $uri/ /index.html;
    }
}

```
