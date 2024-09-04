# 在云服务器配置一个mysql云数据库

> 首先要买好一个服务器，然后就赶紧上手试试把。
>
> 我比较熟悉Ubuntu，所以我就用这个。
>
> 现在我安装的mysql基本都是8.0以上版本了。所以下面的有些语句在5.0无法用。



## 把mysql的root账号变成用密码登录的账号

安装`mysql server`

```bash
sudo apt install mysql-server
```

进入mysql

```bash
mysql
```

修改root账号的plugin（密码验证插件），host（允许登录的主机地址）

```sql
USE mysql;
UPDATE user SET plugin = 'caching_sha2_password', host = '%' WHERE user = 'root';
FLUSH PRIVILEGES;
```

> 你可以验证一下有没有改为caching_sha2_password和%（任意主机）
>
> ```sql
> USE mysql;
> SELECT user,host.plugin FROM user;
> ```

修改root账号的密码为`123456`，因为我们改了密码验证插件，一定要重新改一下密码才行哈

```sql
ALTER USER 'root'@'%' IDENTIFIED BY '123456';
#第一次输入这个语句他会说修改失败，不要紧，再输入一遍就可以了。
#我觉得这个是个bug
```

别忘了更新权限。

```sql
FLUSH PRIVILEGES;
```



## 打开mysql的端口大门。

>  以下两个缺一不可

#### 云服务器的安全组（或者叫防火墙）要打开3306

1. 找到的你云服务器的控制台，配置好安全组，记得要开放3306端口。
2. 不懂就百度搜索，我这里用的是阿里云，所以我搜索`”阿里云安全组配置开放端口”`。这个一定要打开，这是前提。

#### mysql也要关闭绑定地址（bind-address)

打开配置文件

```bash
vi /etc/mysql/mysql.conf.d/mysqld.cnf
```

按字母`i`进入插入模式，前面加上#号注释，输入`:wq`保存文本。

![image-20240705234732232](C:\Users\六件套\AppData\Roaming\Typora\typora-user-images\image-20240705234732232.png)

改了配置文件，一定要重启mysql服务才有效。

```bash
service mysql restart
```

















<hr>

这样，你就完成了服务器的mysql的所有配置，用上公网ip，加上3306端口，在用上root账号和账号密码，去链接试试把。相信这样就能成功

![image-20240705235323781](C:\Users\六件套\AppData\Roaming\Typora\typora-user-images\image-20240705235323781.png)