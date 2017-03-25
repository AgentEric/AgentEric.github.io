---
title: iOS10调用相机crash的问题
comments: true
date: 2016-12-25 20:13:21
tags: iOS
categories:
- 技术
---

> 君子博学而日参省乎己，则知明而行无过矣。

今天遇到一个老项目在 iOS10下 Crash 的问题，研究了一下，终于找到问题源头。iOS10对于App 的授权访问更加严格了，如果调用系统相册、相机功能，或者苹果健康等等没有配置授权请求都会遇到闪退的情况。
调用摄像头的时候，Xcode 控制台输出 Log:

"This app has crashed because it attempted to access privacy-sensitive data without a usage description.  The app's Info.plist must contain an NSCameraUsageDescription key with a string value explaining to the user how the app uses this data."

解决办法：打开 info.plist，输入 Privacy 可以迅速定位到这一权限系列，找到你需要的权限，修改后面的 value 就可以添加相关的访问权限 Key&Value.（Value 是 String 类型的授权描述，可根据不同产品自定义，还可以国际化...）
![info.plist设置.jpeg](http://upload-images.jianshu.io/upload_images/877666-bc2dcf9e9861468b.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

举一反三。

1. Privacy - NSCameraUsageDescription -> 相机权限

   Value: App 需要您的同意才能访问相机

2. Privacy - NSPhotoLibraryUsageDescription -> 相册权限

   Value: App 需要您的同意才能访问相册

3. Privacy - NSMicrophoneUsageDescription -> 麦克风

   …...

4. Privacy - NSContactsUsageDescription -> 通讯录

5. Privacy - NSLocationUsageDescription -> 地理位置

   Privacy - NSLocationWhenInUseUsageDescription->在使用期间访问位置

   Privacy - NSLocationAlwaysUsageDescription->始终访问地理位置

6. Privacy - NSCalendarsUsageDescription->日历

7. Privacy - NSRemindersUsageDescription->提醒事项

8. Privacy - NSMotionUsageDescription->运动与健身

9. Privacy - NSHealthShareUsageDescription->健康分享

10. Privacy - NSHealthUpdateUsageDescription->健康更新

11. Privacy - NSBluetoothPeripheralUsageDescription->蓝牙

12. Privacy - NSAppleMusicUsageDescription->媒体资料库

13. Privacy - Privacy - Speech Recognition Usage Description->语音转文字
好了，以上就是我搜集的隐私相关权限 Key。
___
> 故**不积跬步**，无以致千里；不积小流，无以成江海。
>
> 荀子《劝学篇》

愿你我共进步。
