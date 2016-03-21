
## 前言

### 关键类

* Looper
    + 顾名思义，用于无限循环，在其所属线程中分发消息
    + 分发消息具体解释：从队列中取出消息，并将其传给处理的target
    + Looper的使用
        - Looper有一个MessageQueue的消息队列mQuene
        - Looper.prepare()，在一个线程内只能被调用一次
            * 主要工作：创建一个Looper，并将其和当前线程进行绑定
            * 利用ThreadLocal机制，将Looper和当前线程绑定在了一起
            * Looper.myLooper()可以获取到当前线程的Lopper对象
        - Looper.loop()
            * while(true)无限循环，从mQueue中取出消息Message，并发送给target

* MessageQueue
* Message
* Handler
    + 顾名思义，消息循环时，消息的处理者
    + 我们直接使用的也就是这个类，继承并复写`handleMessage`方法

### 相关类

* ThreadLocal
    + Java的线程局部变量类，全程应该是Thread Local Variable
* HandlerThread

### 参考资料

[[深入理解Android卷一全文-第五章]深入理解常见类 - Innost的专栏](http://blog.csdn.net/innost/article/details/47207951)
[Android消息处理机制(Handler、Looper、MessageQueue与Message)](http://www.cnblogs.com/angeldevil/p/3340644.html)