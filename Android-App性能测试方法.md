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
  * 测试场景
   * 功能测试中监测内存数据
   * 异常情况
     * 内存空间不足
     * 内存使用达到阈值
  * 注意事项
   * 非静态内部类的静态实例容易造成内存泄漏
   * activity使用静态成员
   * 使用handle时的内存问题
   * 注册某个对象后未反注册
   * 集合中对象没清理造成内存泄漏
   * 资源对象没关闭造成内存泄漏

# CPU
 * 工具
  * adb shell
    * dumpsys cpuinfo
    * top
  * DDMS
  * Android Monitor
  * 第三方工具：Emmagee、安测试、腾讯的GT、iTest等

# 电量
 * 工具
  * Battery Historion
    * https://github.com/google/battery-historian (仅Android 5.0以上设备可用)
  * 还可以使用安培仪或第三方软件测量，但都是整机电流变化。
