## 再克隆一个仓库，来熟练使用git



我这里新建了另一个项目

这个项目是**计算器的四则运算**

lxh完成diff（减法功能）

ljt完成divide（除法功能）

nh完成multiply（乘法功能）



下面代码准备好了，每个人只需完成属于自己的功能,再到main函数中如下面调用以下就好了，别多完成。

- nh

  ```c++
  void multiply(int a,int b){
      printf("%d*%d=%d\n",a,b,a*b);
  }
  int main(){
      .......
          if(n==3){
              multiply(a,b);
          }
      .......
  }
  ```

- lxh

  ```c++
  void diff(int a,int b){
      printf("%d-%d=%d\n",a,b,a-b);
  }
  int main(){
      .......
          if(n==2){
              diff(a,b);
          }
      .......
  }
  ```

  

## 注意

**做项目是要严格按照下方模式图**



*这个模式图主分支是main分支（其实很多时候也可能是master分支，这两个是一样的）*

我写这个注意是因为，**我已经在day0长出了ljt分支**，git clone仓库的时候，你会发现你的头指针**HEAD**就会**在ljt分支**上。

看了视频教程，你应该**要自己切换到day0**，**长出属于自己的分支**，然后add-commit-push到远程仓库上。



*这里就不再使用github了，使用的是gitee，流程和**做项目前的准备.pdf**是一样的，*

*也要同意我的邀请，配置ssh，这样你push才不会出问题*



**做项目就用gitee（github很难连上）**