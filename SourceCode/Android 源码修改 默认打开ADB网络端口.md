# Android 源码修改 默认打开ADB网络端口

[链接](https://blog.csdn.net/weixin_42193502/article/details/81491124)

文件在

    android/device/friendly-arm/nanopi2/init.nanopi2.usb.rc

添加以下代码

    on boot
    setprop service.adb.tcp.port 5555
    stop adbd
    start adbd

另外，也可以直接在

    device/friendly-arm/nanopi2/system.prop

中添加

    service.adb.tcp.port=5555

或者在

    build/tools/buildinfo.sh

添加

    echo "service.adb.tcp.port=5555"

云对讲端口写死为9259

最后选择第一个方案
