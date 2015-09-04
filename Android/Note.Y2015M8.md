## 随手笔记

【2015.08】

- 工作上的事情还是很多，自己记录的时间比较少
- 处理的问题也大部分都是业务相关的，与Java、Android相关的也是很少

#### 1.操作Vector的时候，是不是一直是线程安全的呢
- `Vector`虽然是线程安全的，但是通过`Vector.iterator()`得到的`Iterator`却不是！

#### 2.Android对APK的大小有限制吗？

答案是：**有**

**> 那么限制的大小是多少呢**
- Android Developer官网没有找到相关描述，Google BlogSpot发布了一篇博文[《Android Apps Break the 50MB Barrier》](http://android-developers.blogspot.com/2012/03/android-apps-break-50mb-barrier.html)，大概是，之前对APK大小的限制是`50MB`，现在开始可以允许达到`2GB`
- 文章发布时间是2015-03-05，也就大概是`Android3.1 Honeycomb`正式发布前，可以理解为Android 3.1之后，对APK的大小限制提高到了2GB，而在此之前是50MB

**> 虽然Android对APK大小没有限制，但是Google Play以及其他应用分发平台对APK的大小还是有限制的(基本还是50M)**
- 不过Google Play还是允许你attach两个大的(小于2GB)扩展文件，相关链接：[APK Expansion Files](http://developer.android.com/google/play/expansion-files.html)

**> 那么如果在\<3.1的系统安装或运行\>50MB的APK会怎么样呢**
- 尝试了在2.2的模拟器安装一个76.4MB的APK，可以正常运行
- 不过这里占去空间的是assets文件，并不是dex文件，这里说的限制是否实际为此？

**> 听说Android2.3之前对assets目录下单个文件大小有限制(1M)？**
- 相关链接：[Android 常见问题之Assets文件大小限制](http://www.cnblogs.com/jacktu/archive/2012/06/29/2570075.html)

#### 3.发现Youtube上，"Android Developers"有不少干活教程
- [Android Developer主页](https://www.youtube.com/user/androiddevelopers)

#### 4.在Android上避免使用枚举
- [Be aware of memory overhead](https://developer.android.com/training/articles/memory.html#Overhead)
- [The price of ENUMs (100 Days of Google Dev) - YouTube](https://www.youtube.com/watch?v=Hzs6OBcvNQE)

---

- 为什么要限制使用enum呢？
- Rumtime Memory Overhead，运行时内存消耗，这里的Overhead表示消耗/损耗的意思
- enum在Android上的实现是一个类，自己定义的enum类型，其实是继承了java.lang.Enum，它要比常量占用两倍以上的空间
  > Enums often require more than twice as much memory as static constants. 
  > You should strictly avoid using enums on Android.

---

- [IntDef | Android Developers](https://developer.android.com/reference/android/support/annotation/IntDef.html)
- [Support Annotations - Android Tools Project Site](http://tools.android.com/tech-docs/support-annotations)
- [A Look At Android Support Annotations](http://anupcowkur.com/posts/a-look-at-android-support-annotations/)
- Android官方推荐使用注解@IntDef来代替enum，同时又可以防范未定义的int值进行传递
- 另外，如果在项目中使用了Proguard，可以使用它来优化enums(转换成INT values)

```Java
// Sample of @IntDef //
@IntDef({NAVIGATION_MODE_STANDARD, NAVIGATION_MODE_LIST, NAVIGATION_MODE_TABS})
@Retention(RetentionPolicy.SOURCE)
public @interface NavigationMode {}

public static final int NAVIGATION_MODE_STANDARD = 0;
public static final int NAVIGATION_MODE_LIST = 1;
public static final int NAVIGATION_MODE_TABS = 2;

@NavigationMode
public abstract int getNavigationMode();

public abstract void setNavigationMode(@NavigationMode int mode);
```

#### 5.LRUCache的使用
- [The Magic of LRU Cache (100 Days of Google Dev)](https://www.youtube.com/watch?v=R5ON3iwx78M)

```Java
ActivityManager am = (ActivtiyManager)getSystemService(Context.ACTIVITY_SERVICE);
int availMemInBytes = am.getMemoryClass() * 1024 * 1024;
// 这里有一个关键的地方，就是初始大小的分配 //
LruCache bitmapCache = new LruCache<String, Bitmap>(availMemInBytes / 8);
```

#### 6.暂时不知道叫什么
- [The State of LTE (March 2015)](https://opensignal.com/reports/2015/02/state-of-lte-q1-2015/)