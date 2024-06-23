# 统一mysql账户和密码

> 在书写数据库配置文件或者是写JDBC代码的时候，需要输入mysql的账户和密码，但是每个组员的root账户密码都不一样。我们需要另外创建账户

`mysql -u root -p`登录root用户，root用户权限高，能创建用户。

`CREATE USER 'lxhljtnh'@'localhost' IDENTIFIED BY '123456789';`
创建了一个mysql账户，用户名是`lxhljtnh`，密码是`123456789`。

新创建的用户，只是一个小喽喽，并没有权限去看数据库。这也很符合现实的上司下属关系，上司不想给你看的东西，你就是看不到。

所以在`root`下给这个新用户赋权限。
`GRANT ALL ON *.*  TO 'lxhljtnh'@'%'`（这个语句之适用于mysql 8以上版本）
> `*.*`前面的\*代表数据库，后面的\*指的是数据表，\*是一种通配符表示所有的东西
> 比如，myproject.*，指的就是myproject数据库的所有表


最后只有应用刷新后上面的设置才有效`FLUSH PRIVILEGES;`