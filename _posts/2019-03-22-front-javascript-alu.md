---
layout: post
title: 求两个大数相加
category: javascript
tags: [前端]
---

# 求两个大数相加



	const maxNumAdd = function(a, b) {
		//将a、b转化为数字
		let arrA = typeof a === 'number' ? (a + '').split('') : a.split('')
		let arrB = typeof b === 'number' ? (b + '').split('') : b.split('')
		let res = '',
			c = false;
		//只要arrA arrB有数字，就进行相加
		while (arrA.length || arrB.length || c) {
			//boolean值自动转为数字，false位0，true位1，完美解决进位问题
			c += ~~arrA.pop() + ~~arrB.pop()
			res = c % 10 + res
			c = c > 9
		}
		return res.replace(/^0+/, '')
	}






