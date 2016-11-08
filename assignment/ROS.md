#嵌入式 ROS配置
陈益铭 14353042 14C1 Done in [2016.11.8]
##说明
这个实验是配置ROS系统，虽然其中有很多问题，比如说源之类得 艰难险阻还是要做完= =
参考的[网站1](http://wiki.ros.org/cn/jade/Installation/Ubuntu)中文的，还有[网站2](http://blog.csdn.net/qq_32696375/article/details/53066554)做出来的

###Step1:添加Source.list
这个是因为ROS Jade 仅 支持Trusty (14.04)、Utopic (14.10) 和 Vivid (15.04)
>强烈建议换源，把ubuntu的源改为国内的源，这样不管是什么都是快很多= =
>要不然有时候真的很坑爹

```ubuntu
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

###Step2:添加keys
反正跟着教程继续
```
sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-key 0xB01FA116
```

###Step3:一堆安装包
这里需要安装一些东西= =
按顺序来：
1、先是更新下 
```
sudo apt-get update 
```

2、然后是桌面完整版安装： 包含ROS、rqt、rviz、通用机器人函数库、2D/3D仿真器、导航以及2D/3D感知功能
```
sudo apt-get install ros-jade-desktop-full
```

3、初始化rosdep:
```
sudo rosdep init
rosdep update
```

4、环境配置
```
echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

5、安装 rosinstall
```
sudo apt-get install python-rosinstall
```

经过上面一通安装，那么就已经可以用了。
>如果哪个包载不下来，要么用网页找它网站去找，或者更新一下源试试？

###Step4：结果展示
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/ROS-1.jpg">
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/ROS-2.png">
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/ROS-3.png">

##实验总结：
这次实验就是按照网上的教程一步一步下来，遇到问题多多问TA和童鞋，很快就搞定了= =
没想到实验报告这么赶 GG

