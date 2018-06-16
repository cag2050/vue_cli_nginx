### vue-cli 创建的项目，部署在 nginx 上的配置

```
server {
    listen 80;
    server_name xxx.xxx.xxx.xxx;
    charset utf-8;
    root /home/xxx/dist/;
    index index.html;
    location / {
        try_files $uri $uri/ @rewrites; # 需要指向下面的@rewrites，否则会出现vue的路由在nginx中刷新出现404
    }
    # 对应上面的@rewrites，主要原因是路由的路径资源并不是一个真实的路径，所以无法找到具体的文件
    # 因此需要rewrite到index.html中，然后交给路由在处理请求资源
    location @rewrites {
        rewrite ^(.+)$ /index.html last;
    }
    location ~ .*\.(gif|jpg|jpeg|png|bmp|swf|js|css|svg|ttf|otf|eot|woff|woff2)$ {
    	# nginx，如果指定Expires指令，则它会在响应报文中添加Expires和Cache-Control:max-age；nginx默认给静态文件的响应会加上 Last-modified 首部，旧版的nginx不自动带上Etag，nginx认为使用Last-modified已经足够了。
	expires 30d;
    }
}
```
