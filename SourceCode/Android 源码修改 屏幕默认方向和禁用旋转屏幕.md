# Android源码修改 屏幕默认方向和禁用旋转屏幕

[链接1](https://blog.csdn.net/b1480521874/article/details/81204546)

[链接2](https://blog.csdn.net/lizekun2010/article/details/52473571)

在这边同样使用overlay机制去实现

    device/friendly-arm/nanopi2/overlay/frameworks/base/packages/SettingsProvider/res/values/defaults.xml

```xml
<bool name="def_accelerometer_rotation">false</bool>
<!-- Default for Settings.System.USER_ROTATION -->
<integer name="def_user_rotation">0</integer>
```
