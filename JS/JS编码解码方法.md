# JS全局变量之编码解码 

## 1 escape/unescape
	生成新的由十六进制转义序列替换的字符串. 特色字符如: @*_+-./ 被排除在外.
	字符的16进制格式值,当该值小于等于0xFF时,用一个2位转移序列: %xx 表示. 大于的话则使用4位序列:%uxxxx 表示.
	(只能对ASCII符号正确编码)
	
	语法
		escape(str)
	参数
		str
		待编码的字符串.

## 2 encodeURI/decodeURI
	函数通过将特定字符的每个实例替换为一个、两个、三或四转义序列来对统一资源标识符 (URI) 进行编码 (该字符的 UTF-8 编码仅为四转义序列)由两个 "代理" 字符组成)。
	对所有Unicode符号编码

		语法
		encodeURI(URI)
	参数
		URI
		一个完整的URI.
	返回值
		一个新字符串, 表示提供的字符串编码为统一资源标识符 (URI)。

**encodeURI 会替换所有的字符，但不包括以下字符，即使它们具有适当的UTF-8转义序列：<br>
	1. 保留字符	; , / ? : @ & = + $<br>
	2. 非转义的字符	字母 数字 - _ . ! ~ * ' ( )<br>
	3. 数字符号	#**

## 3 encodeURIComponent/decodeURIComponent
	是对统一资源标识符（URI）的组成部分进行编码的方法。它使用一到四个转义序列来表示字符串中的每个字符的UTF-8编码（只有由两个Unicode代理区字符组成的字符才用四个转义字符编码）。
	
	语法
		encodeURIComponent(str);
	参数
		str
		String. URI 的组成部分
_除了字母、数字、(、)、.、!、~、*、'、-和_之外的所有字符。_

## 4 例子
```javascript
var str="http://www.baidu.com/test?hello=你好&world=就是你";
escape(str)
//=> "http%3A//www.baidu.com/test%3Fhello%3D%u4F60%u597D%26world%3D%u5C31%u662F%u4F60"

encodeURI(str)
//=> "http://www.baidu.com/test?hello=%E4%BD%A0%E5%A5%BD&world=%E5%B0%B1%E6%98%AF%E4%BD%A0"

encodeURIComponent(str)
//=> "http%3A%2F%2Fwww.baidu.com%2Ftest%3Fhello%3D%E4%BD%A0%E5%A5%BD%26world%3D%E5%B0%B1%E6%98%AF%E4%BD%A0"
```

## 5 参考
[1 escape MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/escape)<br>
[2 encodeURI MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURI)<br>
[3 encodeURIComponent MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)<br>


