# Android源码修改 默认地区中国 默认语言中文

[链接](https://blog.csdn.net/Nature_Day/article/details/26724327)

在build/tools/buildinfo.sh添加

```shell
echo "persist.sys.language=zh"
echo "persist.sys.country=CN"
echo "persist.sys.timezone=Asia/Shanghai"
echo "ro.product.locale.language=zh"
echo "ro.product.locale.region=CN"
```
