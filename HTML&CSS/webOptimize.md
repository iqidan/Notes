# web性能优化

## 1. 减少http请求
	使用图标合并较少图片请求(图标显示通过显示位置来控制)
	内联图片(直接将图标的base64编码放入文件中)
	多文件合并为一个文件(一般就是js脚本文件和CSS样式文件)

## 2. 使用内容分发服务器(CDN Content Delivery Network)
	一般存放图片/静态组件/静态Html (腾讯cdn使用相关问题借鉴: http://wiki.open.qq.com/wiki/CDN相关常见问题)

## 3. 适当使用缓存功能
	对于长期不改变的组件使用长时间缓存 过期时间设置长时间
```html
	<meta http-equiv="cache-control" content="max-age=360000">
```
	数据包中的格式：

	Cache-Control: cache-directive

	cache-directive可以为以下：

	request时用到：

	| "no-cache"
	| "no-store"
	| "max-age" "=" delta-seconds
	| "max-stale" [ "=" delta-seconds ]
	| "min-fresh" "=" delta-seconds
	| "no-transform"
	| "only-if-cached"
	| "cache-extension"
	response时用到：

	| "public"
	| "private" [ "=" <"> field-name <"> ]
	| "no-cache" [ "=" <"> field-name <"> ]
	| "no-store"
	| "no-transform"
	| "must-revalidate"
	| "proxy-revalidate"
	| "max-age" "=" delta-seconds
	| "s-maxage" "=" delta-seconds
	| "cache-extension"
	部分说明：
	根据是否可缓存分为
	Public  指示响应可被任何缓存区缓存。
	Private  指示对于单个用户的整个或部分响应消息，不能被共享缓存处理。这允许服务器仅仅描述当用户的
	部分响应消息，此响应消息对于其他用户的请求无效。
	no-cache  指示请求或响应消息不能缓存（HTTP/1.0用Pragma的no-cache替换）
	根据什么能被缓存
	no-store  用于防止重要的信息被无意的发布。在请求消息中发送将使得请求和响应消息都不使用缓存。
	根据缓存超时
	max-age  指示客户机可以接收生存期不大于指定时间（以秒为单位）的响应。
	min-fresh  指示客户机可以接收响应时间小于当前时间加上指定时间的响应。
	max-stale  指示客户机可以接收超出超时期间的响应消息。如果指定max-stale消息的值，那么客户机可以
	接收超出超时期指定值之内的响应消息。
	Expires 表示存在时间，允许客户端在这个时间之前不去检查（发请求），等同max-age的
	效果。但是如果同时存在，则被Cache-Control的max-age覆盖。
	格式：
	Expires = "Expires" ":" HTTP-date
	例如
	Expires: Thu, 01 Dec 1994 16:00:00 GMT （必须是GMT格式）
	 
	2.应用
	通过HTTP的META设置expires和cache-control
	<meta http-equiv="Cache-Control" content="max-age=7200" />
	<meta http-equiv="Expires" content="Mon, 20 Jul 2009 23:00:00 GMT" />
	上述设置仅为举例，实际使用其一即可。这样写的话仅对该网页有效，对网页中的图片或其他请求无效，并不会做任何cache。
	这样客户端的请求就多了，尽管只是检查Last-modified状态的东西，但是请求一多对浏览速度必定有影响。
	如果要对文件添加cache可以通过apache的mod_expire模块，写法为
	<IfModule mod_expires.c>
	ExpiresActive On
	ExpiresDefault "access plus 1 days"
	</IfModule>
	记得ExpiresActive设为On，我起先没设置On，似乎怎样YSlow都查不到缓存机制。这样添加的话就是默认所有的。
	如果要针对个别MIME类型则可以：
	ExpiresByType image/gif "access plus 5 hours 3 minutes"
	见 Apache Module mod_expires
	另外，当点击浏览器上的刷新，客户端发送的请求中均是max-age=0，表示validate操作，发送请求到服务器
	要求检查cache，再更新cache，一般得到的是304 Not Modified，表示没变动。

	具体用法
```html
	<meta http-equiv="expires" content="31 Dec 2019">
```
	
## 4. 压缩脚本
	对js/CSS脚本进行压缩,一般使用gzip (查看Accept-Encoding)

## 5. 将样式文件放到head中(首部),将脚本文件到的body中(底部)
	将CSS文件放在head标签中,同时使用link方式引入,JS文件建议放到body底部
	将CSS文件放到body末尾的话可能出现比较长的白屏时间,或者出现Flash of Unstlyed Content问题(无样式内容闪烁)
	JS放到顶部会阻塞后面的下载同时阻塞后面内容的呈现(js可能修改html内容)

## 6. 避免使用CSS表达式
	目前没有用,ie5开始支持,ie8 beta2开始就不支持了,目前无需考虑

## 7. 多使用外部的JS和CSS
	少使用内联的JS和CSS,虽然首次内联方式会比较快,但是外部的JS和CSS是可以缓存的,后续会比较快

## 8. 使用keep-alive和较少的域名以及其缓存
	keep-alive可以重复使用现有连接(也减少了域名查询)
	较少的域名减少DNS的查询, 同样DNS缓存也是减少域名查询

## 9. 精简脚本文件
	对JS和CSS文件进行精简, (对JS可以进行混淆精简,但是可能会带来问题,而且混淆精简和普通精简效果差不多)

## 10. 避免使用重定向
	重定向特别影响性能,增加请求次数
	url结尾少了"/",容易导致重定向"301",URL结尾记得添加"/"(主机名后面确实"/"不会出现重定向, 例如:https://www.baidu.com )

## 11. 避免加载重复的脚步
	加载重复的脚步导致多次执行而影响性能(可能需要多次请求)

## 12. 配置或者移除ETag
	ETAG(Entity Tag)是web服务器和浏览器确认缓存组件有效性的一种机制. 标示服务器上一个组件特定版本的唯一标识. 减少相应的字段. 单台服务器的话推荐,但是集群服务器的话由于不同服务器完全相同的组件的ETAG也不同,因此反而导致不使用原本正确的缓存组件, 这时候比较时候去除ETag比较好,只使用修改时间校验(if-modified-since).

## 13. web大部分时间花在DOM布局之上
	web前端想办法优化DOM布局(CSS) (个人:目前市场上很多以web形式开发的客户端应用 JS这块也是相当重要)


## 14. 异步加载js
	首页延时加载执行js,提升体验, 开始加载必要的js,后续通过js操作dom动态添加script标签,防止某些操作是需要js方法,可以先定义stub函数(同名空函数),防止未下载完需要的js就点击相应操作发生未定义标识符错误.
```javascript
	var domScript = document.createElement("script");
	domScript.src = "script.js";
	document.getElementsByTagName("head")[0].appendChild(domScript);
```
	
	script标签中使用defer和async(https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script)(注意是引入外部脚本)
	defer：用于开启新的线程下载脚本文件，并使脚本在文档解析完成后(DOMContentLoaded事件前)执行。(现在很多浏览器默认就是并行下载js脚本了)
	async：HTML5新增属性，用于异步下载脚本文件，下载完毕立即解释执行代码。

	如果 async="async"：脚本相对于页面的其余部分异步地执行（当页面继续进行解析时，脚本将被执行）
	如果不使用 async 且 defer="defer"：脚本将在页面完成解析时执行
	如果既不使用 async 也不使用 defer：在浏览器继续解析页面之前，立即读取并执行脚本


## 15. 管理好作用域链深度
	查找变量是要遍历作用域链,越往上查找越慢
	使用局部变量, 注意平时创建变量前要加var,不然创建的是全局变量!!访问最慢
	
	with和try catch的catch从句,都是在作用域顶部创建一个对象,会增加访问时间

## 16. 循环遍历优化
	循环次数知道,可以通过总次数递减的方式循环,速度更快,如下
```javascript
	var len = arr.length;
	while(len--){
		doSomethings();
	}
```

	使用Duff策略提升循环效率,总共n次, 一次循环执行m次操作, 需要执行n/m次(n%m需要特殊处理)

	长时间执行的JavaScript,使用定时器将大任务拆分成多个小任务,避免界面假死

## 17. 优化CSS选择器
CSS选择器是 **从右往左进行匹配的, 最右边的限定符称为关键选择** (只要左边还有限定符,就继续匹配,因此 **尽量缩短限定符的个数** !!!), 不是我们目前想象的从左往右匹配, 例如 "#id1 a{}", 不是先找到ID是唯一的id1元素然后找子元素是a的进行应用,而是先找到所有的a元素,然后确认其父元素中有没有ID是id1的!效率很低.
	
	避免使用通配符号(非传统意义的通配符号, 也包括相邻兄弟选择符/子选择符/后代选择符/属性选择符), 推荐使用ID/类/标签选择符号
	对ID选择符号没有必要添加其他限定符号,例如, "div #id2", 直接使用#id2
	不要在类选择符前加标签限定符,而是根据实际情况对类名进行扩展. 例如:li .c1 改为 .li-c1
	选择符越具体越好,限定符越少越棒!! 如ol li .c2 改为 .ol-li-c2
	避免使用后代选择符号,用子选择符号替代 如 ol li 改为ol > li
	避免使用标签-子选择符号,例如#id1 > li > a 直接用 .id1-li-a
	多多使用继承样式




