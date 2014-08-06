---
layout: post
title: matlab结构体
category: 学习
tags: [博客]
---

# matlab结构体

结构(struct)数组

要在MALTAB中实现比较复杂的编程，就不能不用struct类型。而且在MATLAB中实现struct比C中更为方便。

4. 3.1 结构数组的创建
MATLAB提供了两种定义结构的方式：直接应用和使用struct函数。
1. 使用直接引用方式定义结构
与建立数值型数组一样，建立新struct对象不需要事先申明，可以直接引用，而且可以动态扩充。比如建立一个复数变量x：
x.real = 0; % 创建字段名为real，并为该字段赋值为0
x.imag = 0 % 为x创建一个新的字段imag，并为该字段赋值为0 
x = 
real: 0
imag: 0 
然后可以将旗动态扩充为数组：
x(2).real = 0; % 将x扩充为1×2的结构数组
x(2).imag = 0; 
在任何需要的时候，也可以为数组动态扩充字段，如增加字段scale：
x(1).scale = 0; 
这样，所有x都增加了一个scale字段，而x(1)之外的其他变量的scale字段为空：
x(1) % 查看结构数组的第一个元素的各个字段的内容 
ans = 
real: 0
imag: 0
scale: 0 
x(2) % 查看结构数组的第二个元素的各个字段的内容，注意没有赋值的字段为空
ans = 
real: 0
imag: 0
scale: [] 
应该注意的是，x的real、imag、scale字段不一定是单个数据元素，它们可以是任意数据类型，可以是向量、数组、矩阵甚至是其他结构变量或元胞数组，而且不同字段之间其数据类型不需要相同。例如：
clear x; x.real = [1 2 3 4 5]; x.imag = ones(10,10); 

数组中不同元素的同一字段的数据类型也不要求一样：
x(2).real = '123';
x(2).imag = rand(5,1); 
甚至还可以通过引用数组字段来定义结构数据类型的某字段：
x(3).real = x(1); x(3).imag = 3; x(3) 
ans = 
real: [1x1 struct]
imag: 3 
下面看一个实际的例子来熟悉直接引用方式定义与显示结构。

【例4.3.1-1】 温室数据（包括温室名、容量、温度、湿度等）的创建与显示。
（1） 直接对域赋值法产生结构变量  
green_house.name = '一号温室'; % 创建温室名字段 
green_house.volume = '2000立方米'; % 创建温室容量字段
green_house.parameter.temperature = [31.2 30.4 31.6 28.7 % 创建温室温度字段
29.7 31.1 30.9 29.6];
green_house.parameter.humidity = [62.1 59.5 57.7 61.5; % 创建温室湿度字段
62.0 61.9 59.2 57.5]; 
（2）显示结构变量的内容
green_house % 显示结构变量结构 
green_house = 
name: '一号温室'
volume: '2000立方米'
parameter: [1x1 struct] 
green_house.parameter % 用域作用符号. 显示指定域（parameter）中内容 
ans = 
temperature: [2x4 double]
humidity: [2x4 double] 
green_house.parameter.temperature % 显示temperature域中的内容 
ans =
31.2000 30.4000 31.6000 28.7000
29.7000 31.1000 30.9000 29.6000 

【例4.3.1-2】在上例的基础上，创建结构数组用以保存一个温室群的数据。
green_house(2,3).name = '六号温室'; %产生2×3结构数组
green_house % 显示结构数组的结构 
green_house = 
2x3 struct array with fields:
name
volume
parameter 
green_house(2,3) % 显示结构数组元素的结构 
ans = 
name: '六号温室'
volume: []
parameter: [] 

2. 使用struct函数创建结构
使用struct函数也可以创建结构，该函数产生或吧其他形式的数据转换为结构数组。
struct的使用格式为：
s = sturct('field1',values1,'field2',values2,…);
该函数将生成一个具有指定字段名和相应数据的结构数组，其包含的数据values1、valuese2等必须为具有相同维数的数据，数据的存放位置域其他结构位置一一对应的。对于struct的赋值用到了元胞数组。数组values1、values2等可以是元胞数组、标量元胞单元或者单个数值。每个values的数据被赋值给相应的field字段。
当valuesx为元胞数组的时候，生成的结构数组的维数与元胞数组的维数相同。而在数据中不包含元胞的时候，得到的结构数组的维数是1×1的。例如：
s = struct('type',{'big','little'},'color',{'blue','red'},'x',{3,4}) 
s = 
1x2 struct array with fields:
type
color
x 
得到维数为1×2的结构数组s，包含了type、color和x共3个字段。这是因为在struct函数中{'big','little'}、{'blue','red'}和{3,4}都是1×2的元胞数组，可以看到两个数据成分分别为：
s(1,1) 
ans = 
type: 'big'
color: 'blue'
x: 3 
   s(1,2) 
ans = 
type: 'little'
color: 'red'
x: 4 
相应的，如果将struct函数写成下面的形式：
s = struct('type',{'big';'little'},'color',{'blue';'red'},'x',{3;4}) 
s = 
2x1 struct array with fields:
type
color
x 
则会得到一个2×1的结构数组。
下面给出利用struct构建结构数组的具体实例。
