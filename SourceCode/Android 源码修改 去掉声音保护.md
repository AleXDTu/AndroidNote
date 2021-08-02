# Android 源码修改 去掉声音保护

源码目录在

    framework/base/packages/SystemUI/src/com/android/systemui/SafetyWarningDialog.java

另外，可以通过修改 config.xml，目录在

    device/actions/s900_vr/overlay/frameworks/base/core/res/res/values/config.xml

将 config_safe_media_volume_enabled 置 false 来关闭此功能

```xml
<!-- Whether safe headphone volume is enabled or not (country specific). -->
<bool name="config_safe_media_volume_enabled">true</bool>
```

[原文链接](https://blog.csdn.net/ajhsdj/article/details/69569286)