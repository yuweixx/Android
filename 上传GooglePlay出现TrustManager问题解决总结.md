# 上传Google Play出现TrustManager问题解决总结 
## MGA上传Goolge Play未通过审核
8月29日，上传了MGA新版本至Google Play，没多久，收到审核未通过的邮件，具体内容见下图：	
![](http://i.imgur.com/Ae7VFMS.png)
点开[Google Help Center article](https://support.google.com/faqs/answer/6346016)
![](http://i.imgur.com/FUFTD1i.png)
OK,反正有问题，该修改哪些代码呢？
在项目中的代码中搜索“TrustManager”，并没有啊.
## 百度一下
找到了下面的内容：
http://www.cnblogs.com/jinglecode/p/5442740.html
文中提到搜索dump.txt文件，更新或修改第三方的sdk。

## 搜索MGA的dump.txt文件
结果如下：
```
+ Program class: com/umeng/message/proguard/aa$1
  Superclass:    java/lang/Object
  Major version: 0x32
  Minor version: 0x0
    = target 1.6
  Access flags:  0x20
    = class com.umeng.message.proguard.aa$1 extends java.lang.Object

Interfaces (count = 1):
  + Class [javax/net/ssl/X509TrustManager]
```

```
+ Program class: com/crashlytics/android/internal/aH
  Superclass:    java/lang/Object
  Major version: 0x32
  Minor version: 0x0
    = target 1.6
  Access flags:  0x30
    = final class com.crashlytics.android.internal.aH extends java.lang.Object

Interfaces (count = 1):
  + Class [javax/net/ssl/X509TrustManager]
```

```
+ Program class: com/ironsource/mobilcore/aj$1
  Superclass:    java/lang/Object
  Major version: 0x33
  Minor version: 0x0
    = target 1.7
  Access flags:  0x30
    = final class com.ironsource.mobilcore.aj$1 extends java.lang.Object

Interfaces (count = 1):
  + Class [javax/net/ssl/X509TrustManager]
```

哦，是umeng、crashlytics、ironsource相关sdk的问题。

## 再想一下
前几天，DrFone Android也刚在Google Play上上线了新版本，并没有相同的问题啊。
而且DrFone有用到umeng和crashlytics，那MGA的审核未通过应该是ironsource的sdk引起的。
先更新或干掉ironsource的sdk看看吧。

最终选择了简单直接的去掉ironsource的sdk，再次上传Google Play，验证通过，问题解决。

如果下次再遇到相同问题，且是必要的sdk，可以先更新sdk试试。
# Android
