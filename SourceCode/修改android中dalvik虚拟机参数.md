# 修改android中dalvik虚拟机参数

## 说明

最近在了解虚拟机堆空间的参数，扩大APP的运行内存，主要了解几个参数，以及在源码中怎么设置这些值。

## 参数解释

上面说要了解的参数是这几个：

    dalvik.vm.heapgrowthlimit=256m
    dalvik.vm.heapstartsize=64m
    dalvik.vm.heapsize=512m
    dalvik.vm.heaptargetutilization=0.75
    dalvik.vm.heapminfree=1m
    dalvik.vm.heapmaxfree=8m

网上搜索一下，资料挺多的，大概是这样的（我自己理解，不要抠字眼）：

> dalvik.vm.heapstartsize：APP运行的时候分配给虚拟机的初始空间大小
>
> dalvik.vm.heapgrowthlimit：初始分配给APP虚拟机的内存不够用的时候会自动扩张，这个值就是扩张的最大值。（扩张的内存是APP又向系统要的）
>
> dalvik.vm.heapsize：这个值和上一个值的作用差不多，都是APP heap空间的最大值限定，然而这个值是APP使用大heap时的限定值。啥时候使用大heap？就是APP的mainfest文件中有声明 android:largeHeap=“ture”，这个时候，堆空间的最大值使用heapsize限定；没有声明largeHeap的APP，堆空间使用heapgrowthlimit限定。
>
> 这三个值是描述dalvik空间的，剩下三个参数据说是和gc有关的。
>
> dalvik.vm.heaptargetutilization：描述堆内存的利用率，是当前的有效变量所占内存和总内存的比值。
>
> dalvik.vm.heapminfree：描述单次堆内存调整的最小值
>
> dalvik.vm.heapmaxfree：描述单次堆内存调整的最大值

关于这个有很多解释，有一个博客还有个[例子](https://blog.csdn.net/cqupt_chen/article/details/11068129)，老生动了

## imx6平台设置这几个值

在imx6平台我试过在mk文件修改这个配置，之后删除out目录下的build.prop，编译生成的文件中的参数并没有成功修改，这说明在其他地方修改了，把我这个参数覆盖了，然后全局搜索一下，最后发现 frameworks/native/build/tablet-7in-hdpi-1024-dalvik-heap.mk这个文件下的参数配置和我现在的一样，然后修改这个文件，删除out目录下的 build.prop文件，编译之后，发现新生成的 build.prop 文件中 的参数已经改变了，nice

[链接](https://blog.csdn.net/weixin_45349811/article/details/108519810)
