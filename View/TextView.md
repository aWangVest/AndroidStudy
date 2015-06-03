
[TOC]

### android.widget.TextView

1.直接子类和间接子类
- AppCompatTextView `[support.v7]`
- Button
	- AppCompatButton `[support.v7]`
    - CompoundButton
    	- CheckBox
        	- AppCompatCheckBox `[support.v7]`
        - RadioButton
        	- AppCompatRadioButton `[support.v7]`
        - Switch
        - SwtichCompat `[support.v7]`
        - ToggleButton
- CheckedTextView
	- AppCompatCheckedTextView
- Chronometer
- DigitalClock
`[Deprecated in API 17, Replace By TextClock]`
- EditText
	- AppCompatEditText `[support.v7]`
    - AutoCompleteTextView
    	- AppCompatAutoCompleteTextView `[support.v7]`
        - MultiAutoCompleteTextView
        	- AppCompatMultiAutoCompleteTextView `[support.v7]`
    - ExtractEditText
    - SearchEditText `[support.v17]`
- RowHeaderView `[support.v17]`
- TextClock

2.有没有觉得TextView作为基础类，这有多么强大

### 使用时的疑问
1.为什么EditText被继承之后，就没有了焦点状态和输入法光标？
2.到底是哪里控制系统输入法(软键盘)的弹出？
3.TextWatcher的三个回调函数到底是什么关系，分别适用于什么时机，怎么使用？

### 问题解答
1.实在是失误，自己继承EditText的时候，覆盖掉了defStyle，将其设置为0，导致看不到编辑框的效果，包括焦点和输入法光标。其值本来应该为 `android.R.attr.editTextStyle`。其实这里从EditText的源码就可以看出来
``` Java
// 正确的方式 //
public XEditText(Context context, AttributeSet attrs) {
	this(context, attrs, android.R.attr.editTextStyle);
}
// 错误的方式 //
public XEditText(Context context, AttributeSet attrs) {
	this(context, attrs, 0);
}
// EditText源码 //
public EditText(Context context, AttributeSet attrs) {
	this(context, attrs, com.android.internal.R.attr.editTextStyle);
}
```

### 开始研究
1.从哪里入手呢？可以从最常用的方法入手
- 构造方法
- setText
- onDraw

#### 构造方法


[1]:https://developer.android.com/reference/android/widget/TextView.html
[2]:https://developer.android.com/guide/topics/ui/controls/text.html

