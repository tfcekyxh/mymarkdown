# Nginx安装

现在nginx可以直接从apt下载

```shell
sudo apt install nginx
```

nginx通过这个方式下载的，html目录在**`/var/www/html`**中



配置文件可以通过试指令尝试出来

```shell
sudo nginx -t
#或者
whereis nginx
```





<pre>nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
</pre>

所以配置文件是**`/etc/nginx/nginx.conf`**





不知道的指令可以用tldr试试

```
tldr nginx
```



## 常见报错

**mime.types**。用自己写的nginx.conf，缺少mime.types文件

<iframe src="https://blog.csdn.net/weixin_45934749/article/details/127765198" height="700"></iframe>

## 负载分配

```shell
upstream webservers{
	server 192.168.100.128:8080 weight=50;
	server 192.168.100.129:8080 weight=50;
}

server{
	listen 80;
	server_name localhost;
	
	location /api/ {
		proxy_pass http://webservers/admin/;
	}
}
```

