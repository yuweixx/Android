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
     * ``` top ```  查看VSS、RSS
     * ``` dumpsys meminfo packagename/pid ```  查看native进程和java进程
     * ``` procrank ```  只能查看java进程
     * ``` getprop | grep dalvik.vm.heapgrowhlimit ```  查看阈值
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

## CPU
 * 工具
  * adb shell
    * ``` dumpsys cpuinfo ```
    * ``` top ```
  * DDMS
  * Android Monitor
  * 第三方工具：Emmagee、安测试、腾讯的GT、iTest等

## 电量
 * 工具
  * Battery Historion
    * https://github.com/google/battery-historian (仅Android 5.0以上设备可用)
  * 还可以使用安捷伦或第三方软件测量，但都是整机电流变化。

## 流量
 * 测试点
  * 首次启动流量提示
  * 后台运行数小时后流量值
  * 极限操作下流量峰值
  * 运行时流量均值
 * 测试方法
  * 抓包工具：tcpdump、wireshark、charles
  * adb shell (pid和uid的对应关系需要查看/data/system/packages.list，需要root权限)
    * ``` cat /proc/uid_stat/uid/tcp_rcv ```
    * ``` cat /proc/uid_stat/uid/tcp_snd ```
    * ``` cat /proc/net/xt_qtaguid/stats ```
    * Android4.0以下使用 ``` cat /proc/$pid/net/dev ```

## 界面渲染
### 界面过度绘制
* 名词解释：屏幕上某个像素在单个帧中被重绘次数
* 导致问题：应用加载过慢->手机卡死->用户体验变差
* 测试方法：开发者选项中打开"调试GPU过度绘制"->"显示过度绘制区域"

## 磁盘 I/O

### 磁盘I/O性能测试的必要性
- 现阶段移动设备的随机写、随机读性能太差，且长期没有提升

### 主要问题及应对策略
- 主线程 I/O
	- 利用StrictMode排查主线程I/O
- 文件重复 I/O
	- 使用缓存
- 数据库 I/O
	- 优化数据库操作
	- 增加分页大小
	- 减少自增长字段
