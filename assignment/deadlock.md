#Lab4:Deadlock[16.10.19]
主要是了解一下Deadlock的形成原因、解决方案。
1、死锁停在第几次的截图
2、产生死锁的4个必要条件
3、对上述程序产生死锁的解释
##死锁停在第几次的截图
<img src="https://github.com/Ym111/ES2016_14353042/blob/master/Res/Pic/deadlock.png">

根据截图可以看出，死锁停在第211次。
##产生死锁的4个必要条件
死锁就是两个或者多个进程，互相请求对方占有的资源。

1.__互斥条件__：一个资源每次只能被一个进程使用
2.__请求与保持条件__：一个进程因请求资源而阻塞时，对已获得的资源保持不放
3.__不剥夺条件__:进程已获得的资源，在末使用完之前，不能强行剥夺
4.__循环等待条件__:若干进程之间形成一种头尾相接的循环等待资源关系
##对上述程序产生死锁的解释
在main线程中，不断的创建子线程，其中每一个子线程做的事情就是，调用A线程，然后在调用B线程，延迟一段时间，然后开始调用。由于一旦规模扩大起来，那么就会出现两个线程同时调用同一个A或者B的情况，那么这个系统就会进入死锁。

