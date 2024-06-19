### 历经磨难，突然会了MySQL、SQL Server、MySQL Workbench安装
> 系统是Ubuntu23版本
> 如果你和我遇到同样问题，希望可以帮你解决。

### Ubuntu安装`MySQL`

##### 安装MySQL

可以官网下载zip包，自己解压配置。不过我觉得很麻烦，也没学会。大胆输入下面命令。
```shell
sudo apt update
sudo apt install mysql-server
```



##### 启动MySQL

一般安装过程安装完，会自动启动MySQL。我们需要启动MySQL才能修改密码。输入`sudo systemctl status mysql`，你肯定看得懂一点。

如果真的没有自动启动mysql的话，输入`sudo systemctl start mysql`。再输入刚才我讲的命令看看mysql有没有启动。



##### 通过apt安装，MySQL并不会叫你设置用户和密码

所以需要重新设置一下密码，我这里参考了这个视频：[【04-Ubuntu20.04配置最新的Mysql8.0数据库-哔哩哔哩】 https://b23.tv/5JseuP4]( https://b23.tv/5JseuP4)

这里MySQL早就猜到这种情况了，所以给了一个**默认账户**，让我们修改以后最常用到的**root账户**的密码。

我们看一下默认账户的账号和密码`sudo cat /etc/mysql/debian.cnf`，我们需要用到`user`和`password`的两块内容。



##### 记住了账号和密码，我们登陆MySQL，有很多设置。

在终端输入`mysql -u 刚刚看到的user内容 -p`，然后终端会要求你输入密码。你就输入`刚才看到的密码`

登陆默认账户后，大胆复制下面的内容。先不用管这具体是什么样的。
```sql
--root密码验证从auth_socket改成mysql_native_password。你会看到的确发生改变了。

USE mysql;
SELECT user,plugin FROM user;
UPDATE user SET plugin = 'mysql_native_password' WHERE user = 'root';
FLUSH privileges;
SELECT user,plugin FROM user;
```

做完准备工作后**修改密码**吧`ALTER user 'root'@'localhost' IDENTIFIED BY '你想要设置的密码'`。注意密码需要有数字、英文、字符同时满足，至少8位长度，英文字符大小写都要有。如果这个操作有问题（在修改密码前，**不妨试试清空密码**`UPDATE user SET authentication_string='' WHERE user='root';`，再修改）

别忘了`FLUSH privileges`。



##### 退出这个默认账户，登陆我们以后经常用的root账户

输入`exit`退出MySQL，然后输入`mysql -u root -p`，随后输入`你设置的密码`，这样就能登录root账户。

相信做到这里，你能看到welcome字样。



### Windows安装`MySQL`

> 我windows安装还蛮累的，每次都出现Plugin 'mysql_native_password' is not loaded
>
> 自从mysql8.0以后登录验证模式都变了，所以要改回以前的老样子mysql_native_password，但是很容易报上面的错

下载很有门道，如果你每次都会遇到。



### 恭喜你安装完MySQL，`MySQL Workbench`安装很简单的。



##### 在官网下载workbench安装包

直达链接是`https://dev.mysql.com/downloads/workbench/`。
不过直接在`app center`下载就好

没有难度。



### windows安装`SQL Server`

> 现在SQL Server是支持Linux了，我们虽然没有ssms（sql server managagment stdio）这种GUI界面，
>
> 但是jetbrain家DataGrip你可以试试，同样好用。

[Ubuntu安装SQL Server教程：https://learn.microsoft.com/zh-cn/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-ver16&tabs=ubuntu2004](https://learn.microsoft.com/zh-cn/sql/linux/quickstart-install-connect-ubuntu?view=sql-server-ver16&tabs=ubuntu2004)



#### 现在JetBrain制作的`DataGrip`已经足够好用了，可以配置主流数据库

##### datagrip配置mysql

很简单，不用教



##### datagrip配置sql Server

**1.windows下**

总体过程是，打开配置管理器（如果`SQL Server 2022 配置管理器`搜不到，试着搜索`SQL Server configuration manager`），要打开`TCP/IP`协议，然后重新启动`SQL Server`服务，然后去`DataGrip`配置，别忘了用`Windows credentials`验证方式。

<img src="https://s2.loli.net/2024/04/04/T7WOkBXtiHU3a8n.png" alt="sqlserver _3_.png" style="zoom: 67%;" />

<img src="https://s2.loli.net/2024/04/04/B8TcfOySj9X2gQ5.png" alt="sqlserver _1_.png" style="zoom: 67%;" />

<img src="https://s2.loli.net/2024/04/04/evTY82csxzJy4NC.png" alt="sqlserver _4_.png" style="zoom:67%;" />

<img src="https://s2.loli.net/2024/04/04/uhktI2jNwd69ACs.png" alt="sqlserver _2_.png" style="zoom:67%;" />
