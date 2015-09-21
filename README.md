# lucky-card [![license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/Franslee/lucky-card/blob/master/LICENSE) #

lucky-card是一个实现刮刮卡刮奖效果的JavaScript小控件，基于HTML5 Canvas，采用原生js编写，不依赖任何类库，支持AMD/CMD模块化加载，支持iOS、Android和桌面浏览器（IE>=9）,Windows Phone未测。

## DEMO ##

请用手机扫描以下二维码，桌面浏览器可以[点击这里](http://franslee.github.io/lucky-card/demo.html)
#![github](http://franslee.github.io/lucky-card/qr_code.png "lucky-card DEMO") 

## 用法 ##

HTML结构

```html
<div id="scratch">
    <div id="card">￥5000000元</div>
</div>
```

在页面中引入控件所需样式表文件lucky-card.css

```html
<link rel="stylesheet" href="../dist/lucky-card.css">
```
*以上css文件只有控件所必需的样式，刮刮卡样式请根据需要自行编写（可参考DEMO页面）*


引入lucky-card.js/lucky-card.min.js文件

```html
<script src='../dist/lucky-card.js'></script>
```

在确保页面相关DOM加载完毕(*如写在页面底部，或document的DOMContentLoaded事件处理函数中*)之后，初始化控件

```js
LuckyCard.case();
```

## 可配置项与回调函数 ##

初始化lucky-card控件时，支持传入一个JSON对象和(或)一个回调函数，用于配置控件功能/设置回调函数

```js
LuckyCard.case(settings,callback);
```

* 参数settings是一个JSON对象，可选，用于配置控件功能
* 参数callback是回调函数，可选，也可以写在settings中

### 可配置项（settings）一览 ###
<table>
	<tr>
		<th>key</th>
		<th>类型</th>
		<th>默认值</th>
		<th>描述</th>
	</tr>
	<tr>
		<td>coverColor</td>
		<td>string</td>
		<td>"#C5C5C5"</td>
		<td>刮开层的颜色，未设置coverImg时生效，支持十六进制和rgba写法</td>
	</tr>
	<tr>
		<td>coverImg</td>
		<td>string</td>
		<td>""</td>
		<td>刮开层可以是一张图片，在这里设置图片地址，一旦设置此项，coverColor将失效。（注意：图片地址不支持跨域，如果跨域可以考虑将先其转成Data URI）</td>
	</tr>
	<tr>
		<td>ratio</td>
		<td>number</td>
		<td>0.8</td>
		<td>触发回调函数时刮开面积占总面积的比例，超过这个比例回调就触发。建议取值在0到1之间。</td>
	</tr>
	<tr>
		<td>callback</td>
		<td>function</td>
		<td>null</td>
		<td>回调函数，在刮开面积占总面积的比例超过设定值时触发，亦可作为一个独立的参数存在。回调函数内可以调用this.clearCover()方法清除掉刮开层的所有像素。</td>
	</tr>
</table>

```js
//基本用法
LuckyCard.case({coverColor:'#CCCCCC',ratio:.6,callback:function(){alert('中奖啦！')}});

//刮开层支持使用图片，但图片不能跨域，如果跨域可以考虑将先其转成Data URI，再设置
LuckyCard.case({coverImg:'./demo.jpg'});

//callback可作为一个独立的参数存在
LuckyCard.case(function(){
	//清除掉刮开层的所有像素
	this.clearCover();
});
```
