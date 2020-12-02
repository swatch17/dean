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
	
	
	render()
	```
	

- useEffect及其特点
	- 有两个参数：callback和dependencies数组
	- 如果dependencies不存在，那么callback每次render都会执行
	- 如果dependencies存在，只有当它发生了变化，callback才会执行

	```
	let _deps; 
	function useEffect(callback,depArry){
		const hasNoDeps = !depArray; //如果dependencies不存在
		const hasChangeDeps = _deps?!depArray.every((el,i)=>el===_deps[i]):true;
	//	如果dependencies不存在，或者dependencies有变化
		if(hasNoDeps||hasChangeDeps){
			callback();
			_deps = depArray
		}
	}
	```
	
	# 使用数组解决Hooks的复用问题
- 初次渲染的时候，按照useState,useEffect的顺序，把state，deps等按顺序塞到memoizedState数组中
- 更新的时候，按照顺序，从memoizedState中把上次记录的值拿出来
  
  ```
  let memoizedState = [];// hooks存放在这个数组
  let index = 0; //当前memoizedState下标
  
  function useState(initialValue){
	  memoizedState[index] = memoizedState[index]||initialValue;
	  const currentIndex = index;
	  function setState(newState){
		  memoizedState[index++] = newState;
		  render()
	  }
	  return [memoizedState[index++],setState]; //返回当前state,并把index加1
  }
  function useEffect(callback,depArray){
	  const hasNoDeps = !depArray;
	  const deps = memoizedState[index];
	  const hasChangeDeps = deps?!depArray.every((el,i)=>el===deps[i]):true;
	  if(hasNoDeps||hasChangedDeps){
		  callback()
		  memoizedState[index] = depArray;
	  }
	  index++; 
  }
  
  ```
  [参考详情](https://github.com/brickspert/blog/issues/26)