# Android App性能测试方法

## 响应时间
  * 应用启动
   * 冷启动-首次启动
   * 热启动-非首次启动
  * 各页面跳转
  * 测试方法
   * logcat查看activitymanager中，display信息
   * 使用 ```adb shell am -W packagename/.activityname```
   * 也可以用高速摄像机和埋点的方式测试

## 内存
  * 基本概念
   * 栈内存：存放基本数据类型、变量和引用类型变量，由操作系统控制
   * 堆内存：存放由new运行符创建的对象(包括数组)，由程序员控制
  * 工具
   * DDMS
     * 内存监视器
     * 堆内存查看器
     * 内存分配跟踪器
     * http://developer.android.com/intl/zh-cn/tools/debugging/ddms.html
   * ActivityManager.MemoryInfo()
     * Emmagee、安测试、腾讯的GT、iTest等测试工具用的此方法
   * adb shell
     * top  查看VSS、RSS
     * dumpsys meminfo packagename/pid  查看native进程和java进程
     * procrank  只能查看java进程
     * getprop | grep dalvik.vm.heapgrowhlimit  查看阈值
