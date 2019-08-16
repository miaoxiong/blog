---
layout: post
title: css 显示与隐藏
category: css
tags: [前端]
---

# 显示与隐藏

<html>
<head>
	<title>sticky</title>
~<style type="text/css">
		h3{
			margin:0;
		}
		ul,li{
			list-style: none;
			margin:0;
			padding:0;
		}
		.f > .f-d{
			max-height: 0;
			overflow: hidden;
			transition: max-height .4s;
		}
		.f:hover > .f-d{
			max-height: 20px;
		}
		.select{
			width: 128px;
		}
		input{
			box-sizing: border-box;
			width: 100%;
		}
		input:hover ~ .option-wrapper{
			max-height: 150px;
		}
		.option-wrapper{
			background-color:#fcd;
			box-shadow: 5px 5px 2px gray;
			max-height: 0;
			overflow: hidden;
			transition: max-height .4s;
		}
		.s-d{
			opacity: 0;
			filter: Alpha(opacity=0);
		}
		.s:hover > .s-d{
			opacity: 1;
			filter: Alpha(opacity=1);
		}

		.t-d{
			position: absolute;
			opacity: 0;
			filter: Alpha(opacity=0);
		}
		.t:hover > .t-d{
			opacity: 1;
			filter: Alpha(opacity=1);
		}

		.four-d{
			display: none
		}
		.four:hover > .four-d{
			display: block;
		}

		.five-d{
			position: absolute;
			visibility: hidden;
			transform: scale(0);
			transition: all .6s;
		}
		.five:hover > .five-d{
			visibility: visible;
			transform: scale(1);
		}

		.six-d{
			visibility: hidden;
		}
		.six:hover > .six-d{
			visibility: visible;
		}
</style>
</head>

<body>

<h3>1、max-height控制显示与隐藏动画——元素看不见，位置不保留，可以选, 显示位置撑开， 可transition</h3>
<pre>
.code{
  max-height: 0;
  overflow: hidden;
  transition: max-height .4s;
}
li:hover > .code{
  max-height: 20px;
}
</pre>
<div>
	<ul>
		<li class="f">李四<div class="f-d">联系电话：13879641234</div></li>
		<li class="f">张三<div class="f-d">联系电话：15178963254</div></li>
	</ul>
</div>
<div class="select">
	<input value="" placeholder="请选择地方">
	<ul class="option-wrapper">
		<li>学校</li>
		<li>公司</li>
		<li>家</li>
	</ul>
</div>
<h3>2、opacity控制隐藏——单纯的元素看不见，位置保留，可以选</h3>
<pre>
.opacity{
	opacity: 0;
	filter: Alpha(opacity=0);
}
</pre>
<div>
	<ul>
		<li class="s">李四<div class="s-d">联系电话：13879641234</div></li>
	</ul>
</div>
<h3>3、opacity控制隐藏——元素看不见，位置不保留，可以选， 显示位置不撑开</h3>
<pre>
.opacity{
	position:absolute;
	opacity: 0;
	filter: Alpha(opacity=0);
}
</pre>
<div>
	<ul>
		<li class="t">李四<div class="t-d">联系电话：13879641234</div></li>
	</ul>
</div>

<h3>4、display控制隐藏——元素看不见，位置不保留，不可选，有dom资源加载， 显示位置撑开</h3>
<pre>
.dn{
  display: none;
}
</pre>
<div>
	<ul>
		<li class="four">李四<div class="four-d">联系电话：13879641234</div></li>
	</ul>
</div>

<h3>5、visibility 控制隐藏——元素看不见，位置不保留，不可选， 显示位置不撑开， 可transition</h3>
<pre>
.hidden{
  position:absolute;
  visibility:hidden;
</pre>
<div>
	<ul>
		<li class="five">李四<div class="five-d">联系电话：13879641234</div></li>
	</ul>
</div>

<h3 style="margin:0;">6、visibility控制隐藏——元素看不见，位置保留，不可选</h3>
<pre>
.vh{
  visibility:hidden;
}
</pre>
<div>
	<ul>
		<li class="six">李四<div class="six-d">联系电话：13879641234</div></li>
	</ul>
</div>
</body>
</html>






