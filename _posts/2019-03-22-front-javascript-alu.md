---
layout: post
title: 求两个大数相加
category: javascript
tags: [前端]
---

# 求两个大数相加


	const maxNumAdd = function(a, b) {
		let arrA = typeof a === 'number' ? (a + '').split('') : a.split('')
		let arrB = typeof b === 'number' ? (b + '').split('') : b.split('')
		let res = '',
			c = 0;
		while (arrA.length || arrB.length || c) {
			c += ~~arrA.pop() + ~~arrB.pop()
			res = c % 10 + res
			c = c > 9
		}
		return res.replace(/^0+/, '')
	}





