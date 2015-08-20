## 随手笔记

【2015.08】
· 工作上的事情还是很多，自己记录的时间比较少
· 处理的问题也大部分都是业务相关的，与Java、Android相关的也是很少

1.** 操作Vector的时候，是不是一直是线程安全的呢？ **
`Vector`虽然是线程安全的，但是通过`Vector.iterator()`得到的`Iterator`却不是！

2.** Android对APK的大小有限制吗？**
答案是：**有**

** 那么限制的大小是多少呢？**
· Android Developer官网没有找到相关描述，Google BlogSpot发布了一篇博文[《Android Apps Break the 50MB Barrier》](http://android-developers.blogspot.com/2012/03/android-apps-break-50mb-barrier.html)
大概是，之前对APK大小的限制是`50MB`，现在开始可以允许达到`2GB`
· 文章发布时间是2015-03-05，也就大概是`Android3.1 Honeycomb`正式发布前，可以理解为Android 3.1之后，对APK的大小限制提高到了2GB，而在此之前是50MB

** 虽然Android对APK大小没有限制，但是Google Play以及其他应用分发平台对APK的大小还是有限制的(基本还是50M) **
· 不过Google Play还是允许你attach两个大的(小于2GB)扩展文件，相关链接：[APK Expansion Files](http://developer.android.com/google/play/expansion-files.html)

** 那么如果在\<3.1的系统安装或运行\>50MB的APK会怎么样呢？**
· 尝试了在2.2的模拟器安装一个76.4MB的APK，可以正常运行
· 不过这里占去空间的是assets文件，并不是dex文件，这里说的限制是否实际为此？

** 听说Android2.3之前对assets目录下单个文件大小有限制(1M)？ **
· 相关链接：[Android 常见问题之Assets文件大小限制](http://www.cnblogs.com/jacktu/archive/2012/06/29/2570075.html)
