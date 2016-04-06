# host文件修改

 * 需要root权限 ``` su ```
 * 切换到/system/etc目录 ``` cd /system/etc ```
 * 获取/system/etc的读写权限 ``` /system/etc # mount -o rw,remount /system ```
 * 插入想要添加的host内容 ``` echo 192.168.1.1  www.google.com \\n > hosts ```
 
__注：win上修改好的host文件cp到/system/etc是无效的，因为换行符的编码不同。__
