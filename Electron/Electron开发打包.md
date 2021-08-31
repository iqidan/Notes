# Electron开发打包

## 一.需要安装的软件(主要是windows环境):
(nodejs/python的安装 环境变量一定要配置好,尤其是Python的环境!! 配置环境路径的方法: http://jingyan.baidu.com/article/d5a880eb6aca7213f047cc6c.html  简单验证是否全局安装并配置好了: nodejs=>node -v出来版本即可,  Python=>python -h 是否出来帮助提示)

### 1)NodeJS环境安装:https://nodejs.org/download/release/
~~(注意:C:\Program Files\nodejs\node_modules\npm\node_modules\node-gyp\src\win_delay_load_hook.c文件中的”PfnDliHook __pfnDliNotifyHook2 = load_exe_hook;”注释掉, 否则报重复定义错误)~~

### 2)Python安装(建议安装2.7.x, 不要安装3.x.x以及以上版本): https://www.python.org/downloads/windows/

### 3)Visual Studio安装(建议安装最新版本, 注意: 要安装C++编译环境):

### 4)全局安装: 
	1>npm install node-gyp -g 
	2>npm install node-pre-gyp -g (可选)
	3>npm install electron-packager -g


## 二.开发
### 1)搭建项目,初始化项目(根据提示来填写相关信息)
	npm init

### 3)添加Electron依赖
	npm install electron --save-dev


## 三.打包
### 1)打包成可运行的程序
	windows:
	electron-packager ./ iPOS+ --platform=win32 --arch=ia32  
	electron-packager ./ iPOS+ --platform=win32 --arch=x64 
	
	mac:
	electron-packager ./ iPOS+ --platform=darwin --arch=x64 --icon=/Users/iqidan/Node/iPOS+/images/ipos.icns --protocol=ipos+
	
	(electron-packager <sourcedir> <appname> --platform=<platform> --arch=<arch>
	具体查看帮助 electron-packager —help)

	
### 2)制作安装包
	windows制作exe安装包: 使用Inno Setup软件
	mac打包成dmg:electron-installer-dmg  https://github.com/electron-userland/electron-installer-dmg
	例如electron-installer-dmg ./iPos+-darwin-x64/ iPOs+ --icon=/Users/iqidan/Node/iPOS+/images/ipos.icns

## 四.下载Resource Hacker(http://www.angusj.com/resourcehacker/) 
	此软件可修改exe文件中的默认配置(包括图标替换. 安装的程序的运行时名称等等  注意: 此修改在打包后的exe文件上修改, 在打包成安装文件之前)
	备注:
	文件安装的路径最外层名字如:iPOS 是由程序的package.json文件的name字段控制;
	快捷键是有运行的exe文件的productname决定的(用Resource hacker 打开修改)
electron-packager ./ iPosOnline --platform=win32 --arch=x64