# autojs常用语法

获取像需要操作的控件几种方式：

1、id获取。

```
var fasongbtn="com.ss.android.ugc.aweme:id/c55";
var btns = id(fasongbtn).find()。//通过find()查找到的是数组集合。可能会获取到屏幕之外的元素。
let ctrl = ctrls[0], pos = ctrl.bounds(), cx = pos.centerX(), cy = pos.centerY();
click(cx, cy);
```

2、className获取。

```
className("android.widget.FrameLayout").depth(14).indexInParent(4);//通过属性对应的值去获取到具体的元素。
obj.findOnce().click();//必须是获取到的元素的clickable为true。
```

click点击事件。

1、页面元素的clickable为true的调用方式。

```
obj.click();
```

2、页面元素的clickable为false时。

```
click(obj.bounds().centerX(),obj.bounds().centerY())。
```

setText输入内容。

```
setText(idx,content);//idx默认0，默认给第一个输入框赋值。
```

