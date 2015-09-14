# PageSlider #
 
PageSlider 是一个基于zepto.js用于实现H5单页面跟随手指上下滑动切换的组件，支持通过transform3D启动GPU加速，目前仅支持移动端touch设备。

## DEMO ##

请用手机扫描以下二维码,在打开的页面上下滑动查看效果     
#![github](http://franslee.github.io/pageSlider/qr-code.png "pageSlider DEMO") 

## 用法 ##

HTML结构

```html
<!DOCTYPE html>
<html>
	<head>
	  <!-- styles, scripts, etc -->
	</head>
	<body>
		<div class="section sec1"></div>
		<div class="section sec2"></div>
		<div class="section sec3"></div>
		<div class="section sec4"></div>
	</body>
</html>
```

在页面中引入组件所需样式表文件pageSlider.css

```html
<link rel="stylesheet" href="../dist/pageSlider.css">
```

本组件基于zepto，需要在页面中引入zepto.js文件

```html
<script src='http://cdn.bootcss.com/zepto/1.1.4/zepto.min.js'></script>
```

引入pageSlider.js/pageSlider.min.js文件

```html
<script src='../dist/pageSlider.js'></script>
```

在页面DOM加载完毕之后，初始化组件

```js
$(function() {
	var pageSlider = PageSlider.case();
});
```

## 设置 settings ##

初始化PageSlider组件时，支持传入一个参数，用于配置组件功能

```js
PageSlider.case(optOrIndex);
```

* 参数optOrIndex可以是一个数字(number),用于设置初始显示的页码
* 参数optOrIndex也可以是一个json对象，允许的keys见下表

<table>
	<tr>
		<th>key</th>
		<th>类型</th>
		<th>默认值</th>
		<th>描述</th>
	</tr>
	<tr>
		<td>startPage</td>
		<td>number</td>
		<td>1</td>
		<td>初始化时显示页面的页码</td>
	</tr>
	<tr>
		<td>range</td>
		<td>number</td>
		<td>70</td>
		<td>页面回弹的最大距离(像素)，小于该值页面回弹，超过该值页面将切换</td>
	</tr>
	<tr>
		<td>duration</td>
		<td>number</td>
		<td>200</td>
		<td>页面回弹动画持续的时间(毫秒)</td>
	</tr>
	<tr>
		<td>loop</td>
		<td>boolean</td>
		<td>false</td>
		<td>是否循环切换</td>
	</tr>
	<tr>
		<td>elastic</td>
		<td>boolean</td>
		<td>true</td>
		<td>位于顶部(底部)时，是否依然可以向上(向下)拉动</td>
	</tr>
	<tr>
		<td>translate3d</td>
		<td>boolean</td>
		<td>true</td>
		<td>是否使用translate3d(在支持translate3d的设备上)，使用translate3d会使一些设备开启GPU加速，滑动更流畅</td>
	</tr>
	<tr>
		<td>callback</td>
		<td>object</td>
		<td>{}</td>
		<td>页面切换回调函数集合。该json对象每个键为一个数值，对应一个页码，值为一个function,滑动到该页面时触发。如：{2:function(){alert('滑动到了第二页');},4:function(){alert('滑动到了第四页');}} 滑动到第二和第四页时将触发对应的回调函数</td>
	</tr>
</table>

```js
PageSlider.case({loop:true});
```

## 切换到指定页面 ##

在页面初始化后，可调用组件的go方法跳转到指定页面。

```js
//PageSlider初始化
var pageSlider = PageSlider.case();
//跳转到第3页
pageSlider.go(3);
```
