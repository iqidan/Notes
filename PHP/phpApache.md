# PHP的Apache环境配置(Mac) 
[基本环境搭建](https://blog.csdn.net/cgema/article/details/72457985)
[httpd.conf配置文件详解](https://www.cnblogs.com/cqmy/p/6208656.html)
	
## 一. Apache服务操作配置
	(Server version: Apache/2.4.34 (Unix)
	Server built:   Aug 17 2018 16:29:43)
### 1. 基本服务开启关闭
	1）开启Apache  sudo apachectl start	 开启后，可以通过浏览器访问：http://localhost，页面显示“It works” 表示已经成功。
	2）关闭Apache  sudo apachectl stop
	3）重启Apache  sudo apachectl restart

### 2. 配置文件位置
	sudo vi /etc/apache2/httpd.conf
	其中“DocumentRoot”（默认值“/Library/WebServer/Documents”）配置默认访问的位置
	LoadModule用来控制模块加载的

## 二. 使用gizp功能,同时使其能够缓存
	参考:
	启用gzip压缩: https://blog.csdn.net/a757571354/article/details/80362840
	启用gzip导致不能缓存问题解决: https://www.cnblogs.com/baiban/p/5167530.html

### 1. 添加gizp压缩
	前面的注释"#"去掉
	LoadModule headers_module modules/mod_headers.so
	LoadModule deflate_module modules/mod_deflate.so
	LoadModule filter_module modules/mod_filter.so

	添加:
```config
<IfModule mod_deflate.c>
DeflateCompressionLevel 6
AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/html
AddOutputFilterByType DEFLATE text/php
AddOutputFilterByType DEFLATE text/xml
AddOutputFilterByType DEFLATE text/css
AddOutputFilterByType DEFLATE text/javascript
AddOutputFilterByType DEFLATE application/xhtml+xml
AddOutputFilterByType DEFLATE application/xml
AddOutputFilterByType DEFLATE application/rss+xml
AddOutputFilterByType DEFLATE application/atom_xml
AddOutputFilterByType DEFLATE application/javascript
AddOutputFilterByType DEFLATE application/x-javascript
AddOutputFilterByType DEFLATE application/x-httpd-php
AddOutputFilterByType DEFLATE application/x-font-ttf
AddOutputFilterByType DEFLATE image/svg+xml
AddOutputFilterByType DEFLATE image/gif image/jpe image/swf image/jpeg image/bmp
# Don’t compress images and other  #排除不需要压缩的文件
BrowserMatch ^Mozilla/4 gzip-only-text/html
BrowserMatch ^Mozilla/4\.0[678] no-gzip
BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
SetEnvIfNoCase Request_URI .(?:html|htm)$ no-gzip dont-varySetEnvIfNoCase 
#SetEnvIfNoCase Request_URI .(?:gif|jpe?g|png)$ no-gzip dont-vary
SetEnvIfNoCase Request_URI .(?:png)$ no-gzip dont-vary
SetEnvIfNoCase Request_URI .(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
SetEnvIfNoCase Request_URI .(?:pdf|doc)$ no-gzip dont-vary
</IfModule>
```
### 2. 解决gizp压缩导致的不可缓存问题
	前面的注释"#"去掉
	LoadModule headers_module libexec/apache2/mod_headers.so

	添加:
```config
<IfModule mod_headers.c>
#使用gizp导致不能够缓存 解决方法
<FilesMatch "\.(js|css|html|htm|swf|pdf|shtml|xml|flv|gif|ico|jpeg)$">
RequestHeader edit "If-None-Match" "^(.*)-gzip(.*)$" "$1$2"
Header edit "ETag" "^(.*)-gzip(.*)$" "$1$2"
</FilesMatch>
</IfModule>
```

## 备注
1. 查看php信息 phpinfo(); 
2. mac 本地php配置文件路径/private/etc(没有的话复制php.ini.default为php.ini)
