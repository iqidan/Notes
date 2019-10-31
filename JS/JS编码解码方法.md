# JS全局变量之编码解码 

## 1 escape/unescape
	只能对ASCII符号正确编码

## 2 encodeURI/decodeURI
	对所有Unicode符号编码, 
**仅仅对URI的参数部分进行编码
 	对整个URI编码使用**


## 3 encodeURIComponent/decodeURIComponent
	对所有Unicode符号编码
**整个URI编码
	参数部分使用**

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
[1 escape MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/escape)
[2 encodeURI MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURI)
[3 encodeURIComponent MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)


