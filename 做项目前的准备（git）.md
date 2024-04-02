-3.8



## 分享的Git课程我们只需要看这些

每个视频最多8分钟，基本都是4，5分钟的视频

- P2
- P3
- P4
- P5
- P6
- P10
- P11
- P12

下面提到的视频，如果没看懂就要再看一遍，或者来问清楚的，里面的命令行命令要多敲多练。其他的视频二倍速观看也很好懂，视频操作里也是简单的。

P4，P5，P6，P11，P12





## 如果看完了上面的视频，应该知道了一些常见的git命令行

```shell
git init;
git add ...;
git commit (-m "...");


git checkout ...;
//git switch;
git branch;
git branch ...;


git log (--all --decorate --graph);
git status;


//git remote;
//git remote add ...;
git clone ...;
git push；
git pull；
```





## 视频看完，就来一起用一下Git



#### 克隆仓库

我已经在*github*创建了一个仓库（叫*test*），把它这个仓库git clone放入你的电脑里面，然后我们写个超短代码*git*到*github*的仓库里面试试。

这里注意，用git clone克隆下来的仓库，你的本地是知道远程的仓库的。所以不需要担心配置远程仓库。

每个人使用*git* *branch*，分离一个分支，然后到你分离的分支中，这样每个人可以在属于自己的分支中敲代码。

这个仓库里面有一个*test.cpp*。

```shell
你会用到的命令行（用完这个语句，后面就不再用到了）
git clone ...
```



#### 在你克隆的仓库下，做出代码修改

​	1.**我们使用git的正确打开方式应该是**

每个人都从main分支分出属于自己的分支出来写代码，完成完整功能，做了充足debug过后，提交上传到github的仓库。（有的默认的主分支是master分支，都是一样的）

就像下图一样，分支发展后，然后在到第二天把我们三个人的分支再合成到main分支上去。

<img src="/home/ljt/Downloads/_cgi-bin_mmwebwx-bin_webwxgetmsgimg__&MsgID=3444436355933650668&skey=@crypt_25f33897_cbc8c0abc1d2255391c530f19eab6ed5&mmweb_appid=wx_webfilehelper.jpeg" alt="_cgi-bin_mmwebwx-bin_webwxgetmsgimg__&MsgID=3444436355933650668&skey=@crypt_25f33897_cbc8c0abc1d2255391c530f19eab6ed5&mmweb_appid=wx_webfilehelper" style="zoom: 25%;" />

​	

​	2.**所以我们需要从main中长出分支**

> nh已经push了他的版本，你克隆的仓库下来可能HEAD头指针指向的是nh分支，那么你需要切换到main分支
>
> ```shell
> git checkout ... 切换分支
> ```

你已经在main分支下了，就可以git branch长出分支来了

```shell
git branch ... 创建分支
如果你不加上参数，就是显示所有分支，你肯定看得懂的。
```

你已经创建好了分支，如果你用git branch查看过后，发现HEAD头指针并没有指向这个分支，你需要切换分支（上面讲过了）



​	3.**你已经切换到属于你自己的分支，就进行修改提交试试看把**

- 李笑涵

在*test.cpp*写一个函数（叫*LiXiaoHanFunction*）我这里已经准备好了。

```c++
void LiXiaoHanFunction();

void LiXiaoHanFunction(){
	printf("lxh准备就绪\n");
}
main函数调用一下LiXiaoHanFunction
```

- 牛浩

在*test.cpp*写一个函数（叫*NiuHaoFunction*）我这里已经准备好了。

```c++
void NiuHaoFunction();

void NiuHaoFunction(){
	printf("nh准备就绪\n");
}
main函数调用一下NiuHaoFunction
```

每个人在自己分支中的*test.cpp*中做了修改，然后你应该是add commit 再push上去对把（视频教程讲的很详细）（**但是push前我们需要配置东西**。否则git将会告诉你，你没有足够的权限Permission Denied）。



#### 在你push前,你一定要配置一些东西。

- ssh密钥的配置

  ```shell
  windows系统应该直接在此电脑下，生成密钥(我录了个视频，叫ssh.mp4)
  ssh-keygen
  （剩下的步骤，教程已经讲的很清楚了）
  ```

- 你也要告诉组长，把你**加入**到远程仓库**管理员**

  1. **告诉**我你的github绑定的邮箱**或者**用户名（我将会给你发出申请）
  2. 登陆网页github，点击通知，找到我的发的邀请，**同意**加入仓库管理

之后组长在第二天就会叫到一起来，需要git merge合并我们三个人的代码，需要我们三个人保持联系，有冲突的地方每个人应该指出哪里需要保留，哪里需要删除。这样代码就合并完成，然后把这个版本的代码合并到main分支上，之后上传到github 





## 之后就是反复这这样了

每次git的代码就是一个版本，确定做好足够的debug和测试再commit，然后再push到github上。



## 用了git，我们会很常用这些代码

```shell
git checkout
git branch ...
git branch

git add
git commit -m "..."
git push

git fetch
git pull

git log (--all --graph --decorate)
git status
```