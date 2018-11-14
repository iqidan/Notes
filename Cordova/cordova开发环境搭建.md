# Cordova开发环境搭建

## 1. 安装Node环境
	各个平台自行下载(推荐 http://nodejs.cn/download/ )
	
	安装之后可以配置淘宝镜像地址: npm config set registry http://registry.npm.taobao.org/ (配置好后查看: npm get registry)
	
	也可以直接下载cnpm(使用cnpm): npm install -g cnpm

## 2. 开发平台搭建
**先配置JDK** 

下载地址：https://www.oracle.com/technetwork/java/javase/downloads/index.html

（推荐博客： https://blog.csdn.net/callmejeans/article/details/80696107 ）
### 1. Android
	下载AndroidStudio并安装
	(推荐 http://www.android-studio.org/index.php/84-study/ 或 http://www.androiddevtools.cn )	

	安装完后,可能需要配置环境（Mac OS）
	打开终端: 
	vi ~./bash_profile
	输入内容:
	
	export ANDROID_HOME=/Users/iqidan/Library/Android/sdk
	export GRADLE_HOME=/Applications/Android\ Studio.app/Contents/gradle/gradle-3.2 
	exprot PATH=${PATH}:${GRADLE_HOME}/bin
	
	其中”export GRADLE_HOME=/Applications/Android\ Studio.app/Contents/gradle/gradle-3.2 
	”的gradle版本号能会不同, 与Android Studio版本号有关.
(**注意"Android Studio.app"写成 "Android\ Studio.app", 对空格进行转义**)
### 2. iOS
	下载XCode,App Store下载安装即可(很省事)
	
## 3. 配置与使用cordova 
(官方文档 http://cordova.apache.org/docs/en/6.x/guide/cli/index.html )
###	1. 安装cordova 
	npm install -g cordova / cnpm install -g cordova
	(有的需要root权限: sudo npm install -g cordova)
(**注意windows版本的cordova发现需要降低版本，否则创建项目报错 安装6.0.0：cnpm install -g cordova@6.0.0**)
### 2.使用cordova (帮助: cordova -h)
	创建项目,例如:cordova create myApp org.apache.cordova.myApp myApp
	
	添加平台,例如:
		cordova platform add android
		cordova platform add ios
		
    添加插件,例如: cordova plugin add cordova-plugin-camera
    
   	编译,例如:
   		cordova build //全部添加的平台进行编译
		cordova build android //编译android平台
		
	运行,例如:
		cordova run ios/android/browser
		cordova run android -d //debug模式
		
	打包,直接使用相应平台的工具打包.Android使用Android Studio, iOS使用XCode

参考文档:

cordova官方文档注意,开发app: http://cordova.apache.org/docs/en/6.x/guide/cli/index.html

支持插件平台情况: http://cordova.apache.org/docs/en/6.x/guide/support/index.html#core-plugin-apis

cordova_CLI: http://cordova.apache.org/docs/en/6.x/reference/cordova-cli/index.html#cordova-create-command
    
