<!--
 * @Author: Tan Dinbo
 * @Date: 2020-11-16 15:21:28
-->
---
layout: post
title: webpack Loader
tags: [webpack,loader]
renderNumberedHeading: true
grammar_cjkRuby: true
date: 2020-11-16
Author: Dean
comments: true
---
# Loader
 - 实质上webpack loader中的loader就是一个函数，一个声明函数，不能使用箭头函数
 - 这个函数拿到源代码对源代码进一步处理，再返回处理后的源码
 - loader函数中官方推荐使用loader-utils来处理参数
 - 必须要有一个返回值
 - 处理异步时使用this.async，告诉webpack函数内部有异步操纵
 - 在webpack.config.js配置中想要像使用第三方一样使用loader需要配置`resolveLoader`属性解析模块
   

``` javascript
...
resolveLoader:{
modules:["node_modules","./loader"]
}
...
```
- loader解析顺序：自下而上，自右而左