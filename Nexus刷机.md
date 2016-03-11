# Nexus手动刷机

* 很多时候，直接使用官方提供的flash-all.bat或flash-all.sh会刷机失败，这个时候就只好靠手动刷机了，步骤如下：

 ** 1.解压出zip包中的文件。

 ** 2.连接fastboot mode状态的手机，按照以下命令进行刷机。
```shell
#Flash bootloader and radio (radio does not appear on all devices, if it's not in your tgz, you don't need it)

#fastboot flash bootloader <bootloader file name here>.img
#fastboot flash radio <radio file name here>.img

#After flashing the bootloader/radio, you need to reboot the bootloader as shown below, don't skip this step!

fastboot flash bootloader bootloader-shamu-moto-apq8084-71.11.img
fastboot reboot-bootloader
ping -n 5 127.0.0.1 >nul
fastboot flash radio radio-shamu-D4.01-9625-05.16+FSG-9625-02.94.img
fastboot reboot-bootloader
ping -n 5 127.0.0.1 >nul

#Now you can move on to the rest of the files

fastboot flash recovery recovery.img
fastboot flash boot boot.img
fastboot flash system system.img

#NEXUS 9 ONLY - flash this as well

#fastboot flash vendor vendor.img

#If you want to wipe cache and user data (full wipe), flash these

fastboot flash cache cache.img
fastboot flash userdata userdata.img

#Finally, just reboot your device, and Android should start up.

fastboot reboot
```
