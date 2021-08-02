# Ubuntu 16.04 编译 Friendly-arm Android 5.1 源码

2018.09.28

## 搭建编译环境

搭建编译Android的环境建议使用64位的Ubuntu 16.04，安装需要的包即可。

    # sudo apt-get install bison g++-multilib git gperf libxml2-utils make python-networkx zip
    # sudo apt-get install flex libncurses5-dev zlib1g-dev gawk minicom

更多说明可查看[链接](https://source.android.com/source/initializing.html)

## 下载Android5.1源代码

Android源代码的下载需要使用repo，其安装和使用请查看[链接](https://source.android.com/source/downloading.html)

    # mkdir android && cd android
    # repo init -u https://github.com/friendlyarm/android_manifest.git -b nanopi2-lollipop-mr1
    # repo sync

## 编译系统

    # source build/envsetup.sh
    # lunch aosp_nanopi2-userdebug
    # make -j8

注：编译之前需检查清楚 Python 版本和 Java 版本，Python 使用的是 ***2.7*** 的，Java 使用的是 ***openJdk7***  
切换版本命令如下

    # sudo update-alternatives --config java
    # sudo update-alternatives --config javac
    # sudo update-alternatives --config javadoc

    # sudo update-alternatives --config python

切换版本后记得运行命令：

    # make update-api

进行更新
***
若要重新编译，则可以先

    # make clean

若遇到 aidl_language_l.l 相关错误，可以输入

    # export LC_ALL=C

PS：记得要用bash去编译！
