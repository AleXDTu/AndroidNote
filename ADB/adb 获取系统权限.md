# adb 获取系统权限

可以使用以下命令获取系统权限

```shell
# adb root
# adb connect 10.11.11.11
# adb remount
```

另外，shell进去以后，可以用cat命令打印build.prop

```shell
# cat /system/build.prop
```

还可以直接添加参数

```shell
# adb shell ro.secure=0>>/system/build.prop
```

要记得修改权限

```shell
# adb shell chmod 644 /system/build.prop
```

然后重启

```shell
# adb shell reboot
```

如果提示只读可尝试

```shell
# mount -rw -o remount /system // 以读写权限重新挂载system
```

PS：记录一下 adb 的位置

设备的话是

```shell
/sbin/adbd
/system/bin/adb
```

Android 源码在

```shell
/system/core/adb/
```
