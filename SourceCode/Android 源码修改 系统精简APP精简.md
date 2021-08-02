# Android源码修改 系统精简APP精简

修改以下文件

    device/firendly-arm/nanopi2/device.mk
    build/target/product/core.mk
    build/target/product/full_base.mk
    build/target/product/generic_no_telehoney.mk
    build/target/product/sdk_base.mk

可能有些apk经过以上的方法还是不能真正的去掉，这个时候我们需要理清模块被包含在哪些mk文件中

举个例子，如果我需要移除Browser浏览器app，那么可以通过如下的指令

    find ./ -name "*.mk" | xargs grep "Browser" --color=auto

先查找到哪些mk包含了Browser，然后逐一删除掉。
