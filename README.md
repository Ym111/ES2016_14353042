[TOC]
#嵌入式系统 实验
陈益铭 14353042 14C1 begin in [2016.9.28]
###lab1 DOL配置过程 [16.9.28]
实验配置DOL文件

####step1：虚拟机
安装unbuntu虚拟机
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/1.png">
如图安装好虚拟机
>本人计算机使用WIN10系统，使用VMP12版本,ubuntu是16.0.4，64位的版本

####step2：更新ubuntu
使用
``` 
    sudo apt-get update
    sudo apt-get install ant
    sudo apt-get install openjdk-7-jdk
    sudo apt-get install unzip
```
更新系统的必要环境
>其中有一些注意事项：
最好一开始就使用中科大的源
怎么换源，可以百度下
如果openjdk-7jdk不能安装，很可能就是源的问题

那么结果大概就会如下图：
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/2.png">
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/3.png">
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/4.png">
>图中就是没有成功安装openjdk-7-jdk,换源之后就搞定了

####step3：解压&编译

新建dol的文件夹
```
   mkdir dol
```
将dolethz.zip解压到 dol文件夹中
```
   unzip dol_ethz.zip -d dol
```
解压systemc
```
   tar -zxvf systemc-2.3.1.tgz
```
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/5.png">
解压后进入systemc-2.3.1的目录下
```
   cd systemc-2.3.1
```
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/6.png">
新建一个临时文件夹objdir
```
   mkdir objdir
```
进入该文件夹objdir
```
   cd objdir
```
运行configure(能根据系统的环境设置一下参数，用于编译)
```
   ../configure CXX=g++ --disable-async-updates
```
编译
```
   sudo make install
```
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/7.png">
编译完后文件目录如下()，能看到include, lib-linux64(对于32位系统，这里是lib-linux
```
 cd ..       
```
记录当前的工作路径(会输出当前所在路径，记下来，待会有用)
```
   pwd
```
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/8.png">

####step4：编译DOL
进入刚刚dol的文件夹
```
   cd ../dol
```
修改build_zip.xml文件
找到下面这段话，就是说上面编译的systemc位置在哪里，
<property name="systemc.inc" value="YYY/include"/>
<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
把YYY改成上页pwd的结果
>注意，对于64位 系统的机器，lib-linux要改成lib-linux64）

然后是编译
```
   ant -f build_zip.xml all
```
若成功会显示build successful
接着可以试试运行第一个例子
进入build/bin/mian路径下
```
   cd build/bin/main
```
然后运行第一个例子
```
   ant -f runexample.xml -Dnumber=1
```
成功结果如图
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/9.png">

####lab1实验感想
对于这次实验，是最基础的配置实验，那么其实难度并不大，主要的问题是在遇到问题怎么去解决。其实在遇到那个jdk不能安装的时候，去群里咨询了下，发现换源能够解决，那么就要自己去百度怎么样才能换源，达到比较好的下载速度，然后就自己根据网上的教程一通配置，发现执行指令就可以了。所以遇到问题还是需要多讨论，然后就可以比较快地完成实验。
此致 第一次实验结束。

###lab2 版本控制&MD的使用 [16.9.29]
这部分是第二次实验要求，主要是在ubuntu上能够使用GIT来管理文件。

####step1：安装GIT
对于ubuntu系统，简直友好的不要不要的，直接使用指令
```
    sudo apt-get install git
```
自己就下载好了。然后你需要的是去[GIT](https://github.com/)官网注册一下
然后创建自己的一个仓库 ，获得一个URL 
然后在ubuntu创建一个对应的文件夹
```
    git init +url
```
就会在当前位置创建一个文件夹，用来同步
使用以下指令进行登陆
```
    git
```
然后就可以提交自己的文档上去。

####step2：README.md编写
这部分使用markdown进行编写README文件，推荐几个在线网站[ MUHUA ](http://mahua.jser.me/)很不错的在线编辑网站

语法部分呢，可以参考[Wiki-Markdown](https://en.wikipedia.org/wiki/Markdown)里面讲的挺多的。
这次文本也是使用Markdown进行编写的。所以感觉很不错

####lab2实验感想
这次实验主要是体验一下GIT的好用和Markdown的好用，估计以后很多都会使用这个来编写，确实要好好学习这个编写软件，排版出来确实很清爽，大爱。至于GIT的使用，可能一开始还不得要领，所以觉得并没有什么优势，虽然之前已经听到很多人推荐这么去管理文件了，所以还是希望能够早点体会到git的好用，早点上道，做好一个程序员。
大概就是这样了
至此 第二次实验结束。


