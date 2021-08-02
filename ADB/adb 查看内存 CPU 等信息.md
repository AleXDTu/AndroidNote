# adb 查看内存、CPU 等信息

## 查看内存

    adb shell dumpsys meminfo
    // 查看某apk的内存
    adb shell dumpsys meminfo <包名>
    // 或者
    adb shell dumpsys meminfo pid
    // 比如：查看com.duowan.mobile
    adb shell dumpsys meminfo com.duowan.mobile
    // 另外还有一个命令
    adb shell procrank

说到内存，不得不说下内存的各个参数：

> - VSS - Virtual Set Size 虚拟耗用内存（包含共享库占用的内存）是单个进程全部可访问的地址空间。
> - RSS - Resident Set Size 实际使用物理内存（包含共享库占用的内存）是单个进程实际占用的内存大小，对于单个共享库，尽管无论多少个进程使用，实际该共享库只会被装入内存一次。
> - PSS - Proportional Set Size 实际使用的物理内存（比例分配共享库占用的内存）。
> - USS - Unique Set Size 进程独自占用的物理内存（不包含共享库占用的内存）USS 是一个非常非常有用的数字，因为它揭示了运行一个特定进程的真实的内存增量大小。如果进程被终止，USS 就是实际被返还给系统的内存大小。USS 是针对某个进程开始有可疑内存泄露的情况，进行检测的最佳数字。怀疑某个程序有内存泄露可以查看这个值是否一直有增加。
>
> 一般情况：VSS>= RSS >= PSS >= USS。

我们经常说的内存占用一般指的是 PSS 实际使用的物理内存.

## 查看 cpu

    adb shell top -m 10 -s cpu // 按照 cpu 排序，显示前10个
    // 或者
    adb shell dumpsys cpuinfo

## 查看电池电量

    adb shell dumpsys battery

## 查看某 apk 的流量

1. 首先先查出该 apk 的 uid
    - `ps`一下找到应用的 pid
    - 拿到 pid 后，直接查看`/proc/$pid/status`这个文件下，存储了 uid
2. 然后通过 uid 查看`/proc/uid_stat/$uid/tcp_rcv`和`/proc/uid_stat/$uid/tcp_snd`，这两个文件一个是请求耗费的流量，一个是接受的数据流量
3. 如果想算速率，可以这么计算
    - 先拿这两个参数，然后间隔 10s
    - 再拿这两个参数，两次参数之差再除以 10s，就是这 10s 的平均速率。

[原文链接](https://www.jianshu.com/p/6eca57b5885e)
