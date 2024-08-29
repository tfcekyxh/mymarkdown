# 注意注意DLL其实很容易使用

> 我这里用的dll文件，我取了一个名叫`os.dll`，对应的lib文件也叫`os.lib`

## Visual Studio使用dll文件

直接在`cpp文件`中加入（是cpp文件哈）

```c++
#pragma comment(lib，"os.lib") //这是静态的连接库
//但是lib和dll都不能缺少，要放在一起，这样就引用了dll
```

别忘了如果没有函数的声明，记得把声明写出来，让编译器知道有这个函数。



## Clion使用dll

其实Clion中，如果安装了Cmake那就会默认使用Cmake。

我这里用的也是Cmake，所以要通过`cmakeList.txt`来配置dll。

请在`cmakelist.txt`加上下面的东西

```
#（1/2）
#引入一个文件夹目录，这里就会包扫描cmake-build-debug文件夹。
#这一句要在add_executable()前
include_directories(./cmake-build-debug) 


#（2/2）
add_library(项目名称 os.dll)
#项目名称就抄add_executable括号里面的第一个单词就好了。
#这一句要在add_executable()后面
```

这样就配置好了一个dll的连接。



## Clion配置后，<u>**发现一点击运行控制台就闪退？**</u>

如果你发现一点击运行就是`exit code with -1037151515`这样的。

那就是`dll文件`和`可执行文件`不在同一个目录下。放在一起就可以了。

（这也就是我为什么把`os .dll`放在`cmake-build-debug`这个文件里面了。因为编译产生的可执行文件就是在这个文件夹。

**解决方法**

1. 把dll文件放在可执行文件同一个目录下。
2. `edit configuration` - `environment variables` 中添加一个变量叫做`PATH`，`PATH`的值就是`os.dll`所在的文件目录路径

### 

