# Maven工具开发网站项目

> 我们做大作业的项目**如果只使用git**，每切换一次历史commit，我的项目文件夹就发生了改变，**这要在idea中重新导jar包**。
> 
> 使用maven可以免去这个麻烦，并且方便web项目的传递。
> 
> 你也知道git中移除一个已经追踪（tracked）的文件，再git add-commit-push提交，再merge合并分支，不是一件容易的事

Maven经常用于Java项目的构建和依赖管理。以下是一些常见的`Maven配置`和使用：

idea专业版自带maven（bundled maven 或 mave-wrapper），这里要使用bundled maven（这个不用设置，idea默认就是这个）。

## 配置
### 打开idea的全局设置。
如果你一启动idea就打开了一个项目，**一定一定请关闭项目**，到这样子的界面打开设置。

![1](https://s2.loli.net/2024/03/29/Dfckm87BzHOLQTR.png)

### 修改`setttings.xml`并应用到idea的maven中（配置阿里巴巴maven中央仓库）
idea自带的maven**没有提供settings.xml**，我们自己新创建一个settings.xml（我放在c盘根目录下了）

这是**我自己用的配置文件，大胆复制吧**。里面配置好了阿里云maven仓库。

```xml
<!-- 
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
 -->
<!-- 
 | This is the configuration file for Maven. It can be specified at two levels:
 |
 |  1. User Level. This settings.xml file provides configuration for a single user,
 |                 and is normally provided in ${user.home}/.m2/settings.xml.
 |
 |                 NOTE: This location can be overridden with the CLI option:
 |
 |                 -s /path/to/user/settings.xml
 |
 |  2. Global Level. This settings.xml file provides configuration for all Maven
 |                 users on a machine (assuming they're all using the same Maven
 |                 installation). It's normally provided in
 |                 ${maven.conf}/settings.xml.
 |
 |                 NOTE: This location can be overridden with the CLI option:
 |
 |                 -gs /path/to/global/settings.xml
 |
 | The sections in this sample file are intended to give you a running start at
 | getting the most out of your Maven installation. Where appropriate, the default
 | values (values used when the setting is not specified) are provided.
 |
 | -->
<settings xmlns="http://maven.apache.org/SETTINGS/1.2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 https://maven.apache.org/xsd/settings-1.2.0.xsd">
<!--  localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
   -->
<!--  interactiveMode
   | This will determine whether maven prompts you when it needs input. If set to false,
   | maven will use a sensible default value, perhaps based on some other setting, for
   | the parameter in question.
   |
   | Default: true
  <interactiveMode>true</interactiveMode>
   -->
<!--  offline
   | Determines whether maven should attempt to connect to the network when executing a build.
   | This will have an effect on artifact downloads, artifact deployment, and others.
   |
   | Default: false
  <offline>false</offline>
   -->
<!--  pluginGroups
   | This is a list of additional group identifiers that will be searched when resolving plugins by their prefix, i.e.
   | when invoking a command line like "mvn prefix:goal". Maven will automatically add the group identifiers
   | "org.apache.maven.plugins" and "org.codehaus.mojo" if these are not already contained in the list.
   | -->
<pluginGroups>
<!--  pluginGroup
     | Specifies a further group identifier to use for plugin lookup.
    <pluginGroup>com.your.plugins</pluginGroup>
     -->
</pluginGroups>
<!--  TODO Since when can proxies be selected as depicted?  -->
<!--  proxies
   | This is a list of proxies which can be used on this machine to connect to the network.
   | Unless otherwise specified (by system property or command-line switch), the first proxy
   | specification in this list marked as active will be used.
   | -->
<proxies>
<!--  proxy
     | Specification for one proxy, to be used in connecting to the network.
     |
    <proxy>
      <id>optional</id>
      <active>true</active>
      <protocol>http</protocol>
      <username>proxyuser</username>
      <password>proxypass</password>
      <host>proxy.host.net</host>
      <port>80</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
     -->
</proxies>
<!--  servers
   | This is a list of authentication profiles, keyed by the server-id used within the system.
   | Authentication profiles can be used whenever maven must make a connection to a remote server.
   | -->
<servers>
<!--  server
     | Specifies the authentication information to use when connecting to a particular server, identified by
     | a unique name within the system (referred to by the 'id' attribute below).
     |
     | NOTE: You should either specify username/password OR privateKey/passphrase, since these pairings are
     |       used together.
     |
    <server>
      <id>deploymentRepo</id>
      <username>repouser</username>
      <password>repopwd</password>
    </server>
     -->
<!--  Another sample, using keys to authenticate.
    <server>
      <id>siteServer</id>
      <privateKey>/path/to/private/key</privateKey>
      <passphrase>optional; leave empty if not used.</passphrase>
    </server>
     -->
</servers>
<!--  mirrors
   | This is a list of mirrors to be used in downloading artifacts from remote repositories.
   |
   | It works like this: a POM may declare a repository to use in resolving certain artifacts.
   | However, this repository may have problems with heavy traffic at times, so people have mirrored
   | it to several places.
   |
   | That repository definition will have a unique id, so we can create a mirror reference for that
   | repository, to be used as an alternate download site. The mirror site will be the preferred
   | server for that repository.
   | -->
<mirrors>
<!--  mirror
     | Specifies a repository mirror site to use instead of a given repository. The repository that
     | this mirror serves has an ID that matches the mirrorOf element of this mirror. IDs are used
     | for inheritance and direct lookup purposes, and must be unique across the set of mirrors.
     |
    <mirror>
      <id>mirrorId</id>
      <mirrorOf>repositoryId</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
      <url>http://my.repository.com/repo/path</url>
    </mirror>
      -->
<mirror>
<id>aliyunmaven</id>
<mirrorOf>*</mirrorOf>
<name>阿里云公共仓库</name>
<url>https://maven.aliyun.com/repository/public</url>
</mirror>
</mirrors>
<!--  profiles
   | This is a list of profiles which can be activated in a variety of ways, and which can modify
   | the build process. Profiles provided in the settings.xml are intended to provide local machine-
   | specific paths and repository locations which allow the build to work in the local environment.
   |
   | For example, if you have an integration testing plugin - like cactus - that needs to know where
   | your Tomcat instance is installed, you can provide a variable here such that the variable is
   | dereferenced during the build process to configure the cactus plugin.
   |
   | As noted above, profiles can be activated in a variety of ways. One way - the activeProfiles
   | section of this document (settings.xml) - will be discussed later. Another way essentially
   | relies on the detection of a property, either matching a particular value for the property,
   | or merely testing its existence. Profiles can also be activated by JDK version prefix, where a
   | value of '1.4' might activate a profile when the build is executed on a JDK version of '1.4.2_07'.
   | Finally, the list of active profiles can be specified directly from the command line.
   |
   | NOTE: For profiles defined in the settings.xml, you are restricted to specifying only artifact
   |       repositories, plugin repositories, and free-form properties to be used as configuration
   |       variables for plugins in the POM.
   |
   | -->
<profiles>
<!--  profile
     | Specifies a set of introductions to the build process, to be activated using one or more of the
     | mechanisms described above. For inheritance purposes, and to activate profiles via <activatedProfiles/>
     | or the command line, profiles have to have an ID that is unique.
     |
     | An encouraged best practice for profile identification is to use a consistent naming convention
     | for profiles, such as 'env-dev', 'env-test', 'env-production', 'user-jdcasey', 'user-brett', etc.
     | This will make it more intuitive to understand what the set of introduced profiles is attempting
     | to accomplish, particularly when you only have a list of profile id's for debug.
     |
     | This profile example uses the JDK version to trigger activation, and provides a JDK-specific repo.
    <profile>
      <id>jdk-1.4</id>

      <activation>
        <jdk>1.4</jdk>
      </activation>

      <repositories>
        <repository>
          <id>jdk14</id>
          <name>Repository for JDK 1.4 builds</name>
          <url>http://www.myhost.com/maven/jdk14</url>
          <layout>default</layout>
          <snapshotPolicy>always</snapshotPolicy>
        </repository>
      </repositories>
    </profile>
     -->
<!-- 
     | Here is another profile, activated by the property 'target-env' with a value of 'dev', which
     | provides a specific path to the Tomcat instance. To use this, your plugin configuration might
     | hypothetically look like:
     |
     | ...
     | <plugin>
     |   <groupId>org.myco.myplugins</groupId>
     |   <artifactId>myplugin</artifactId>
     |
     |   <configuration>
     |     <tomcatLocation>${tomcatPath}</tomcatLocation>
     |   </configuration>
     | </plugin>
     | ...
     |
     | NOTE: If you just wanted to inject this configuration whenever someone set 'target-env' to
     |       anything, you could just leave off the <value/> inside the activation-property.
     |
    <profile>
      <id>env-dev</id>

      <activation>
        <property>
          <name>target-env</name>
          <value>dev</value>
        </property>
      </activation>

      <properties>
        <tomcatPath>/path/to/tomcat/instance</tomcatPath>
      </properties>
    </profile>
     -->
</profiles>
<!--  activeProfiles
   | List of profiles that are active for all builds.
   |
  <activeProfiles>
    <activeProfile>alwaysActiveProfile</activeProfile>
    <activeProfile>anotherAlwaysActiveProfile</activeProfile>
  </activeProfiles>
   -->
</settings>
```

![12](https://s2.loli.net/2024/03/29/vMVHeXdNCoqkRx8.png)

![2](https://s2.loli.net/2024/03/29/nU6pWMmI7kBPALz.png)


### 修改maven本地仓库位置（可做可不做）
通过maven下载的jar包，实际就是从中央仓库下载到本地仓库。默认的本地仓库位置，我觉得不好看。就是上图的local_repository修改一下， 改成自己喜欢的位置。

只要修改了`settings.xml`，其实配置就完成了。下面你可以使用一下。

## 开始使用
我们这里创建一个`mysql`数据库连接的项目。如果成功了就输出ok。
我们需要用maven添加`mysql驱动jar包（mysql-connector）`

### 使用maven创建javaEE（jarkarta）项目

![3](https://s2.loli.net/2024/03/29/RdkcgmVoLPBGCAq.png)

![4](https://s2.loli.net/2024/03/29/SA39FxR1G84Cgdz.png)


### 用maven导入jar包（添加依赖）
首先，maven第一次导入mysql的驱动包。我们先去官网的maven仓库搜索，然后一般选择使用人数最多的版本。复制下来。

![5](https://s2.loli.net/2024/03/29/oMiC9EUbGqxrFNe.png)

![6](https://s2.loli.net/2024/03/29/MZ5fIOgkcE7DuAj.png)

![7](https://s2.loli.net/2024/03/29/VAZpROnbcQxkzU4.png)

![8](https://s2.loli.net/2024/03/29/5yUNCgzwRYZuLmj.png)

在`POM.xml`中粘贴就可以了。这段导入依赖的语句一定要被`<dependencies></dependencies>`包裹。现在这个语句是红色的。

![9](https://s2.loli.net/2024/03/29/s7XuVQ3t4rc9qB8.png)

右上角会出现一个小图标，你点击一下，maven就会给你下载并导入依赖了。

## 测试导入依赖是否成功

刚才不是点了`maven图标`嘛。现在创建新的类，我这里叫`JDBC`。试试下面代码。

![10](https://s2.loli.net/2024/03/29/AjTEOIXgSLHmq2J.png)



## 恭喜你成功了

![11](https://s2.loli.net/2024/03/29/cFvwtdLZPKb7gfT.png)

maven除了能导入依赖，甚至可以将web项目打成war包方便，在有maven的电脑上通过war包部署你的maven项目。添加依赖只是其中maven的冰山一角。



## 我遇到的问题

idea其实有的时候有点bug，**即便是**全局设置了maven。有的时候你的新建项目不是使用`bundled maven`。你可以看一下这个`.mvn`这个文件夹，有没有`maven-wrapper.jar`，如果有的话，自己通过`File - Setting - Maven`设置成`maven（bundled）`即可