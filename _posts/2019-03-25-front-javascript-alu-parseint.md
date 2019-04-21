---
layout: post
title: parseInt的实现
category: javascript
tags: [前端]
---

# parseInt的实现

#要求：输入为字符串或者数字，转化为特定进制的数字

#不考虑字母的情况
	const parseInt1 = function(str, radix) {
	//输入为非数字和字符串 则返回NaN
	if (typeof str !== 'number' && typeof str !== 'string')
		return NaN;

	let toStr = ('' + str).trim()
	let srcStr = toStr.split('.')[0]
	let len = srcStr.length
	//转化部分为空则返回NaN
	if (len === 0)
		return NaN;
	//进制为0,undefined,null 则默认转为10
	if (!radix) {
		radix = 10;
	}

	let res = 0;
	// 进制在2到36之间
	if (radix < 2 || radix > 36)
		return NaN;

	for (let i = 0; i < len; i++) {
		// 转化到当前位无效时，则返回有效部分，否则返回NaN
		if (srcStr[i] >= radix && res > 0) {
			return res
		} 
		else if (srcStr[i] >= radix && res == 0) {
			return NaN
		}
		res = radix * res + ~~srcStr[i]
	}
	return res;
		}

#改进版 考虑字母的情况

	const parseInt2 = function(str, radix) {
	//输入为非数字和字符串 则返回NaN
	if (typeof str !== 'number' && typeof str !== 'string')
		return NaN;
	let toStr = ('' + str).trim()
	let srcStr = toStr.split('.')[0]
	let len = srcStr.length
	//转化部分为空则返回NaN
	if (len === 0)
		return NaN;
	//进制为0,undefined,null 则默认转为10
	if (!radix) {
		radix = 10;
	}

	let res = 0;
	if (radix < 2 || radix > 36)
		return NaN
	for (let i = 0; i < len; i++) {
		//非字母或者数字直接退出循环
		let reg = /[a-z]|[A-Z]|\d/g
		if (!reg.test(srcStr[i]))
			break;
		let elem = srcStr.charCodeAt(i);
		//小写字母
		if (elem >= 97) {
			elem -= 87
		//大写字母
		} else if (elem >= 65) {
			elem -= 55
		//数字
		} else {
			elem -= 48
		}
		if (elem >= radix) {
			//首位就大于进制则返回NaN
			if (i === 0) {
				return NaN;
			}
			break;
		}
		res = radix * res + elem
	}
	return res;
}





