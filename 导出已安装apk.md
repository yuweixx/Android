# 导出已安装apk
 * 1.启动要导出的app；
 * 2.使用 ``` adb shell dump activity activities　``` 查看app安装信息；
 * 3.找到 ``` packageName=xxx.xxx.xxx ... baseDir=/data/app/xxx.xxx.xxx-x/base.apk ``` 的信息；
 * 4.利用 ``` adb pull /data/app/xxx.xxx.xxx-x/base.apk xxx.apk ``` 导出想要的apk文件。

