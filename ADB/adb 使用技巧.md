# ADB 使用技巧

## ADB命令指定设备

    C:\Users\gaojs>adb devices
    List of devices attached
    emulator-5554   device
    4dfadcb86b00cf05        device

给命令加上-s的参数即可指定设备

    C:\Users\gaojs>adb -s emulator-5554 shell

## ADB offline状态

ADB本身的BUG所导致的，可用如下的方法处理：

    C:\Users\gaojs>adb kill-server
    C:\Users\gaojs>taskkill /f /im adb.exe

第一条命令是杀ADB的服务，第二条命令是杀ADB的进程

如果第一条没有用，才考虑用第二条命令

***
[原文链接](https://blog.csdn.net/gaojinshan/article/details/9455193)
