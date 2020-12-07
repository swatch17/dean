---
title: JS常用工具方法
tags: [Object,type]
renderNumberedHeading: true
grammar_cjkRuby: true
author: Dean
---
### 判断数据类型

``` javascript
 function getType（type）{
	var str = Object.prototype.toString.call(type);
	return str.slice(str.index(' ')+1,str.length-1).toLowerCase()
}
```