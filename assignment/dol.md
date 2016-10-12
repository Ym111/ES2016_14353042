
###Lab3 DOL实例分析&编程[16.10.12]
第三次实验，主要是了解DOL的性质，其中明白每一个函数的意义，熟悉一下编程的过程，通过简单的代码修改，实现对任务基本要求。

####step1：代码修改
根据example给出的图例

<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/3-5.png">

那么可以看出整个的结构主要有3部分，生产者、中间者、消费者这三个基本的块，那么查看src的文件夹发现.c .h文件，就是这一个实验的重点，其中每一部分就是对应的框架。

其中每一个.c文件内，都有一个init函数和fire函数，其中Init函数只是运行一次，然后fire函数类似于LOOP，能够在程序中不断得执行，直到结束。
然后每一个块进行定义，每一个块单独设置里面得程序，比如进行一个平方，像这样得进行操作。然后实例化出几个实例化，那么剩下的部分就是--连接

.xml文件定义了连接，其中可以对前面创建的实例进行实例化，可以使用迭代省去大部分的工作，重复进行
```
<variable value="2" name="N"/> //<----------------------------------------//

  <!-- instantiate resources -->
  <process name="generator">
    <port type="output" name="10"/>
    <source type="c" location="generator.c"/>
  </process>

  <iterator variable="i" range="N">
    <process name="square">
      <append function="i"/>
      <port type="input" name="0"/>
      <port type="output" name="1"/>
      <source type="c" location="square.c"/>
    </process>
  </iterator>
```
这里是更改了迭代次数，同时布局的时候。迭代2次，那么就可以完成任务1，因为变成i^4，所以就可以了。这里也是DOL的一个很大的特性，把功能的定义和连接的定义分开去定义，这样把每一个模块定义好，设定好功能，在通过.xml文件进行调用，实例化、设置彼此的关系。这就是DOL的编译特点。通过更改了迭代次数，那么获得如下的结果。

<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/3-2.png">

对应的example2的dot为

<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/3-7.png">
那么这个获得的结果正确之后，完成任务2就可以更加简单，主要的更改在于，模块的设置，因为模块里面是平方的操作，那么我们只要改为i^3就可以，调用的模块因为.xml只调用1次，所以直接更改即可
```
int square_fire(DOLProcess *p) {
    float i;

    if (p->local->index < p->local->len) {
        DOL_read((void*)PORT_IN, &i, sizeof(float), p);
        i = i*i*i;  //<------------------------------------------------//
        DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
        p->local->index++;
    }

    if (p->local->index >= p->local->len) {
        DOL_detach(p);
        return -1;
    }

    return 0;
}

```
那么就可以获得如下结果：

<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/3-1.png">

那么example1的dot图为

<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/3-6.png">

####step2: 遇到的问题
这一次实验中遇到的最大问题是，更改了square.c之后，却不能获得效果。所以查看build文件夹内的main/可以看到，example1是锁定状态，证明不能进行修改，所以我们要做的是把对应的文件夹删除（我是这么进行处理的）所以提高权限，使用
```
    su root
```
获得ROOT权限，这样就可以使用
```
    rm -rf +文件夹名称
```
就可以删除对应的文件夹，这样重新使用ant -f runexample.xml函数，重新进行build
####lab3实验感想
本次实验，由于上课TA讲的很清楚，同时对于PDF编写也很用心，对于代码的解读已经完成得差不多。所以根据TA所给得提示，很快就可以实现对应功能。一开始以为会有其他得问题，但是发现真的只要更改一两个数值就可以完成本次实验，所以实验感想就没有多写了，主要是在代码修改的部分加上我的想法、理解。
至此第三次实验完成。
