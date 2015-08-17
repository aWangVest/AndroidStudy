
## Android官方废弃的方法、类、常量

1.** The constructor BitmapDrawable(Bitmap) is deprecated **

This constructor was deprecated in API level 4. Use BitmapDrawable(android.content.res.Resources, android.graphics.Bitmap) instead to specify a bitmap to draw with and ensure the correct density is set.

说明：需要替换成`BitmapDrawable(Resources, Bitmap)`，保证生成的Drawable分辨率是正确的

http://stackoverflow.com/questions/9978884/bitmapdrawable-deprecated-alternative
http://developer.android.com/reference/android/graphics/drawable/BitmapDrawable.html

---
<p>
2.** The method setBackgroundDrawable(Drawable) from the type View is deprecated **

``` Java
public void setBackground(Drawable background) {
	//noinspection deprecation
	setBackgroundDrawable(background);
}

/**
* @deprecated use {@link #setBackground(Drawable)} instead
*/
@Deprecated
public void setBackgroundDrawable(Drawable background) {
	// ... ... //
}
```

说明：这似乎只是命名的问题，Stackoverflow上有人在讨论

http://stackoverflow.com/questions/13729675/difference-between-setbackgrounddrawable-and-setbackground/13729733#13729733

下面这个链接给了一个方案，使用setBackgroundResource代替setBackgroundDrawable，但是，这是事实上并不靠谱，要是我只有Drawable，没有ID怎么办哇

http://www.crifan.com/android_the_method_setbackgrounddrawable_drawable_from_the_type_view_is_deprecated/

---
<p>
3.** The constructor NeighboringCellInfo() is deprecated **

说明：NeighboringCellInfo的相关信息获取不应该是通过创建NeighboringCellInfo的对象来获取，而是选择传入一个location的String进行解析`NeighboringCellInfo(int rssi, String location, int radioType)`，或者通过`TelephonyManager.getNeighboringCellInfo()`得到

http://stackoverflow.com/questions/3868223/null-issue-with-neighboringcellinfo-cid-and-lac
http://developer.android.com/reference/android/telephony/gsm/GsmCellLocation.html
http://developer.android.com/reference/android/telephony/NeighboringCellInfo.html

---
<p>
4.** The field Build.VERSION.SDK is deprecated **

说明：关于怎么获取Android版本号的问题，在Stackoverflow上也得到了很多的讨论
`Build.VERSION.SDK_INT在API4`及以上版本添加的
`Build.VERSION.SDK`是一直都有
但是在这里我觉得可以不用考虑Android1.5的设备了

http://developer.android.com/reference/android/os/Build.VERSION.html#SDK_INT
http://stackoverflow.com/questions/3423754/retrieving-android-api-version-programmatically

---
<p>
5.** The field Context.MODE_WORLD_READABLE is deprecated **

说明：顾名思义，就是全世界都可以读的模式，我晕，怎么会有这种代码在项目里面。你就算是需要共享数据，可以用Provider啊！这里不讨论了

http://developer.android.com/reference/android/support/v4/content/FileProvider.html

---
<p>
6.** The field PhoneStateListener.LISTEN_SIGNAL_STRENGTH is deprecated **

`@deprecated by {@link #LISTEN_SIGNAL_STRENGTHS}`

说明：Listen for changes to the network signal strengths (cellular).
用来获取信号强度的，但是LISTEN_SIGNAL_STRENGTHS是API7才添加的，这一点需要酌情

http://developer.android.com/reference/android/telephony/PhoneStateListener.html#LISTEN_SIGNAL_STRENGTHS

