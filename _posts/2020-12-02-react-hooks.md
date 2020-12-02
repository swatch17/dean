---
layout: post
title: React Hooks实现
date: 2020-12-02
Author: Dean
categories: 
tags: [react, hooks,useState]
comments: true
---
- useState

	```
	// 代码中通常的应用，给函数组件中的变量赋值
	import React,{useState} from 'react'
	...
	const [value,setValue] = useState('');
	/*
	*value为变量名称
	*setValue为改变变量的方法
	*value的值只能通过setValue方法去改变
	*/
	```