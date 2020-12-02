---
layout: post
title: React Hooks实现
date: 2020-12-02
Author: Dean
categories: 
tags: [react, hooks,useState,useEffect]
comments: true
---
- useState

	```
	// 代码中通常的应用，给函数组件中的变量赋值
	import React,{useState} from 'react'
	...
	const [value,setValue] = useState('');
	
	/*
	* value为变量名称
	* setValue为改变变量的方法
	* value的值只能通过setValue方法去改变
	* useState('')为value设置初始值
	*/
	
	// 简单实现
	let _state; //把state存储在外面
	
	function useState(initialValue){
		_state = _state||initialValue;
		function setState(newState){
			_state = newState;
			render();
		}
		return [_state,setSate]
	}
	
	function render(){
		ReactDOM.render(<div>{value}</div>,document.getElementById('root'))
	}
	
	```
	

- useEffect及其特点
	- 有两个参数：callback和dependencies数组
	- 如果dependencies不存在，那么callback每次render都会执行