# Android NDK 运行错误：java.lang.UnsatisfiedLinkError: Couldn't load XXX indLibrary returned null

## 方法1

直接将so文件放到了Android Studio的默认路径 src > main > jniLibs

## 方法2

修改jniLibs的默认路径为libs：

```gradle
android {
    sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
    }
}
```

[原文链接](https://blog.csdn.net/yy1300326388/article/details/46291417)
