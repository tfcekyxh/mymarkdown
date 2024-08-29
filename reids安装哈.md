# 我的个人尝试安装redis

> 我使用的是Ubuntu，发现apt里面就已经有了redis，不妨就直接用这个试试。

安装`redis`

```shell
sudo apt install redis
```

修改一下`redis`的配置文件，不过apt安装你不知道配置文件在哪。用`whereis`查找一下

```shell
whereis redis
```

一般进入配置文件所在目录或者要修改配置文件，都是需要很高的权限的。这里使用`su`切换至root用户进行操作哈。

```shell
su
cd [刚刚whereis查找出来的目录]
vi ./redis.conf
```





改配置文件要注意一下，我觉得这两个就很重要了

```redis.conf
bind 0.0.0.0					   #要监听任意地址
daemonize yes					   #后台守护进程开启
requirepass [这里写你要设置的密码]	#别忘了设置密码
```



**你可能其实不知不觉的就运行了redis，找到他的pid杀死他。**

```shell
ps -ef | grep redis
kill [redis的pid]	#如果没有，那就直接下一步呗
```

再重新用配置文件启动redis，就可以了。

```shell
redis-server ./redis.conf
```





#### 设置开机启动

首先就是自定义一个服务。一般我们都放在`/etc/systemd/system/`里面。这里还是需要高权限哈。

```shell
cd /etc/systemd/system
```



自己使用`vi`命令新建一个`redis.service`。如果发现已经有了这个service，那就直接修改这个文件，这就更轻松了。

`redis.service`里面一定要有这个就行

```redis.service
[unit]
[service]
Type=forking	#Type一定要是forking，不要是notify。如果不行就试试删掉这个Type=forking
ExecStart=/usr/bin/redis-server /etc/redis/redis.conf	#不要多加东西，这一行
[install]
Alias=redis.service
```



千万**别忘了重启守护进程**，检测一下我们新写的服务。这样我们的`redis.service`这个服务就注册好了。

```shell
systemctl daemon-reload
```

这样就可以使用`systemctl`来启动了，这里启动一下，看看会不会出错

```shell
systemctl start redis
```

> 如果这里报错Configuration错误，自己去好好修改`redis.service`。注意格式，或者一些属性配置。

最后别忘了设置开机启用

```shell
systemctl enable redis.service
```







#### 设置开机自动启动报错解决方案



- 这里启用发现报错，错误是**不允许开机启动一个link文件**。所以要找到原来的文件。

<pre><strong>root@ljt:/etc/systemd/system# systemctl enable redis.service</strong> 
<font color="#C01C28">Failed to enable unit: Refusing to operate on alias name or linked unit file: redis.service</font>
</pre>  




- 查找一下这个redis.service到底是何方神圣。找到本体然后启动。这里找到的本体是`redis-server.service`。所以启用他就好了

<pre><strong>root@ljt:/etc/systemd/system# ll |grep redis</strong> 
lrwxrwxrwx  1 root root   40  8月  1 20:33 <font color="#C01C28"><b>redis</b></font>.service -&gt; /lib/systemd/system/<font color="#C01C28"><b>redis</b></font>-server.service<br>
<strong>root@ljt:/etc/systemd/system# systemctl enable redis-server.service</strong>
Synchronizing state of redis-server.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable redis-server
</pre>

