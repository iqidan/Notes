# Nodejs版本管理工具 [n](https://www.npmjs.com/package/n)
	

## 1. 安装n
```
	npm install -g n
	//或
	make install
```

## 2. 常用命令
	n                              显示已安装的Node版本(显示后上下键选择 enter确认切换版本 q退出)
	n latest                       安装最新版本Node
	n stable                       安装最新稳定版Node
	n lts                          安装最新长期维护版(lts)Node
	n <version>                    根据提供的版本号安装Node

## 注意
* n不支持Windows windows建议使用[nvm-windows](https://github.com/coreybutler/nvm-windows/releases)
* nvm使用请参考[Windows 下多版本 NodeJS 安装和管理](https://www.jianshu.com/p/128f52787f48)
