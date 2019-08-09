---
layout: post
title: echarts柱状图数字太小无法点击的解决方案
category: javascript
tags: [前端]
---

# echarts柱状图数字太小无法点击的解决方案

#背景：虽然echarts提供了click事件，但是如果柱状图数字太小，无法点击到柱形图，可通过下面的解决方案。



	let self = this;
    this.chart.getZr().on('click', (params) => {//添加点击事件
      let pointInPixel= [params.offsetX, params.offsetY];//获取鼠标的x和y的位置
      if (self.chart.containPixel('grid',pointInPixel)) {
		//将位置转化为具体的dataIndex
        let dataIndex =self.chart.convertFromPixel({seriesIndex:0},[params.offsetX, params.offsetY])[0];
        let {xAxis} = self.chart.getOption()
        let disCode = xAxis[0]['data'][dataIndex].disCode
        //处理业逻辑
      }
    })






