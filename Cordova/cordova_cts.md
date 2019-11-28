# 周大生项目

## 创建项目: 
    cordova create CTSIShop com.chowtaiseng.ishop 周大生
    (将iOS的ID在项目中手动改为 com.chowtaisengpro.ishop 由于原来周大生打包证书的原因)


    baison测试
    cordova create ChowTSCordova org.baison.chowtscordova ChowTSCordova
    (将iOS的ID在项目中手动改为 com.baison.chowtscordova 由于我们公司通用打包证书的原因)

## 添加平台:
    cordova platform add ios
    cordova platform add android

## 添加插件:
### 一. 百度定位:
    cordova plugin add cordova-plugin-baidumaplocation --variable ANDROID_KEY="YOUR_KEY" --variable IOS_KEY="YOUR_PID" 
    

    baison测试
    cordova plugin add cordova-plugin-baidumaplocation --variable ANDROID_KEY="YOUR_KEY" --variable IOS_KEY="YOUR_PID"
    
    (Android安装后有问题
    切换到Project=>
    1 找到app/BaiduLBS_Android.jar 选中右击 选中"add as library"
    2 找到app/src/com 下的aruistar拖动到app/src/main/java/com下


    )

### 二. 支付宝:
    cordova plugin add https://github.com/DmcSDK/cordova.plugin.alipay.git --variable PID=YOUR_PID


    baison测试 
    cordova plugin add https://github.com/DmcSDK/cordova.plugin.alipay.git --variable PID=YOUR_PID
    
    (Android 
    切换到Project=>
    找到app/libs/alipaySdk - **.jar 选中右击 选中"add as library"
    )

### 三. 微信登录 微信支付:
    cordova plugin add cordova-plugin-wechat --variable wechatappid=YOUR_PID

    baison测试
    cordova plugin add cordova-plugin-wechat --variable wechatappid=YOUR_PID

    (iOS
    linker command failed with exit code 1
    解决办法: 打开xcode -> 打开项目 -> General -> Link Binary With Libraries
    找到libc++6并删除，添加 libc++.1.tbd

    Android
    切换到Project=>
    找到 src/包名全路径/wxapi 将wxapi文件夹剪切到 app/src/main/java/包名全路径/
    本程序 scr/org/baison/chowtscordova/wxapi => app/src/main/java/org/baison/chowtscordova/

    修改plugins/cordova-plugin-wechat/scripts/android-install.js中
```javascript
    var targetDir  = path.join(projectRoot, "platforms", "android", "src", packageName.replace(/\./g, path.sep), "wxapi");
```
    =>
```javascript
    var targetDir  = path.join(projectRoot, "platforms", "android", "app", "src", "main", "java", packageName.replace(/\./g,    path.sep), "wxapi");
```
 

~~修改CordovaLib/src/org/apache/cordova/cordovaPlugin.java
    protected CordovaPreferences preferences; => protected static CordovaPreferences preferences;~~

    获取签名
    cd ~/.android 
    =>
    keytool -list -v -keystore debug.keystore(自己jks文件路径)
    如: keytool -list -v -keystore /Users/iqidan/Desktop/p12/android/baison_android.jks 
    签名错误了后面修改请参照进行操作: https://blog.csdn.net/KisenHuang/article/details/73770863

    正式:
    keytool -list -v -keystore /Users/iqidan/Desktop/p12/android/cts/cts.keystore -alias chowtaiseng -storepass CTs1213141516 -keypass YOUR_KEYPASS
    )


### 四. 二维码扫描:
    cordova plugin add phonegap-plugin-barcodescanner ANDROID_SUPPORT_V4_VERSION="24.1.0"
    (
    界面有些丑陋,需要修改
    )

### 五. 震动:
    cordova plugin add cordova-plugin-vibration

### 六. 设备信息(iOS Android)
    cordova plugin add cordova-plugin-device
    
### 七. 剪贴板功能
    cordova plugin add cordova-clipboard

支付
https://github.com/DmcSDK/cordova.plugin.alipay

登录：
https://github.com/iVanPan/Cordova_QQ
https://github.com/xu-li/cordova-plugin-wechat
https://github.com/iVanPan/cordova_weibo




