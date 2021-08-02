# Android源码修改 屏幕常亮和开机不锁屏

[链接](https://blog.csdn.net/lizekun2010/article/details/52473571)

同样使用overlay机制  
目录在

    device\friendly-arm\nanopi2\overlay\frameworks\base\packages\SettingsProvider\res\values\defaults.xml

```xml
<integer name="def_screen_off_timeout">600000</integer> // 改为-1

<!-- https://blog.csdn.net/ztguang/article/details/72857009 -->

<bool name="def_lockscreen_disabled">false</bool> // 改为true

<!-- https://blog.csdn.net/wz_sky/article/details/52021781 -->
```

Java源码目录在

    frameworks/base/services/core/java/com/android/server/power/PowerManagerService.java

```java
private int getScreenOffTimeoutLocked(intsleepTimeout) {
    int nosleep;
    int timeout = mScreenOffTimeoutSetting;
    if(isMaximumScreenOffTimeoutFromDeviceAdminEnforcedLocked()) {
        timeout = Math.min(timeout,mMaximumScreenOffTimeoutFromDeviceAdmin);
    }
    if(mUserActivityTimeoutOverrideFromWindowManager >= 0) {
        timeout = (int)Math.min(timeout,mUserActivityTimeoutOverrideFromWindowManager);
    }
    if (sleepTimeout >= 0) {
        timeout = Math.min(timeout,sleepTimeout);
    }
    nosleep = mScreenOffTimeoutSetting;
    if(nosleep < 0)
    {
        nosleep = mMaximumScreenOffTimeoutFromDeviceAdmin;
        return Math.max(nosleep,mMaximumScreenOffTimeoutFromDeviceAdmin);
    }
    return Math.max(timeout,mMinimumScreenOffTimeoutConfig);
}
```

以上方法最大只能是24.5天不灭屏，现做如下修改：

```java
private void updateUserActivitySummaryLocked(long now, int dirty) {
    …
    // 2021-04-19 永远让mUserActivitySummary为屏幕亮，时间设置为Long的最大值
    mUserActivitySummary = USER_ACTIVITY_SCREEN_BRIGHT;
    nextTimeout = Long.MAX_VALUE;
    Message msg = mHandler.obtainMessage(MSG_USER_ACTIVITY_TIMEOUT);
    msg.setAsynchronous(true);
    mHandler.sendMessageAtTime(msg, nextTimeout);
    
    // if (mUserActivitySummary  != 0 && nextTimeout >= 0) {
        // Message msg = mHandler.obtainMessage(MSG_USER_ACTIVITY_TIMEOUT);
        // msg.setAsynchronous(true);
        // mHandler.sendMessageAtTime(msg, nextTimeout);
    // }
    …
}
```

以下方案没有找到文件

[链接](https://www.jianshu.com/p/ec7aa61a6c51)

开机不锁屏

    frameworks/base/policy/src/com/android/internal/policy/impl/KeyguardViewMediator.java // 未找到

```java
/**
 * External apps (like the phone app) can tell us to disable the keygaurd.
 */
private boolean mExternallyEnabled = true; // 改为 false
```
