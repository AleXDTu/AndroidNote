# Android源码修改 隐藏系统状态栏和导航栏

[链接](https://blog.csdn.net/lizekun2010/article/details/52473571)

## 隐藏系统状态栏

目录在

    device/actions/s900_vr/overlay/frameworks/base/core/res/res/values/dimens.xml

```xml
<dimen name="status_bar_height">0dip</dimen>
```

## 隐藏系统导航栏

目录在

    device/actions/s900_vr/overlay/frameworks/base/core/res/res/values/config.xml

```xml
<bool name="config_showNavigationBar">false</bool>
```

> 注意：此处使用了Overlay机制

另外，修改系统状态栏还可以在

    frameworks/base/packages/SystemUI/src/com/android/systemui/statusbar/phone/PhoneStatusBar.java

修改：

```java
boolean panelsEnabled() {
    //return (mDisabled & StatusBarManager.DISABLE_EXPAND) == 0;
    return false;
}
```
