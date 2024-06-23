# Ubuntu的tomcat安装很简单
## 安装tomcat
去tomcat官网下载安装包，由于我们是`ubuntu`所以下载`tar.gz`包，双击压缩包解压，把文件夹移动到你想安装的路径。（我这里移动到`~`目录）。这样你就安装完了。

这里下载要提一嘴，**<u>不要下载src，没有编译过</u>**。肯定要下载一个版本，只要不是src的版本（源码版本）就行。其他的都是编译过，的所以可以直接部署用。





## 本地启动安装的tomcat
找到`bin`目录，进入目录，使用终端输入`sudo ./startup.sh`，这样`tomcat`就打开了。

如果你不放心，你可以输入`sudo systemctl status tomcat`来查看tomcat服务是否启动好。

或者直接在浏览器输入`http://localhost:8080`







## 如果要idea配置tomcat
> idea不能使用社区版，一定要用专业版。我使用的版本
> - jdk1.8
> - tomcat8
> 两个版本对应了，都是8

1，打开Idea专业版，新建一个jakarta项目


2，找到，点击add，填写`Tomcat Home`和`Tomcat base directory`

只需要在`tomcat home`选项和`tomcat base directory`选项填写tomcat路径/usr/local/tomcat/apach-tomcat-8.xxxxx。你就可以点击完成了。（如果你报错了，下面有解决方法）

3，如果你报错：`The selected directory is not a valid Tomcat home`。

解决方法：只需要**给**tomcat安装目录足够的用户组**权限**就好。

```bash
a)输入`sudo chmod 777 ./apach-tomcat-8.xxxx`
  
b)重启idea（“一定要重启！！！！”，这样idea才能发现自己有足够权限去使用tomcat里面的东西了）
  
c)再重复上面步骤，最后你应该成功了。
```

4，你成功配置了！







## idea测试启动tomcat
自己new一个jarkarta项目，一开始就要选中使用web application选项。

然后，点击下一步使用对应的tomcat的版本，勾不勾选下面的一堆东西都无所谓。

