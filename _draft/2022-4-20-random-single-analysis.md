---
title: 随机信号分析复习笔记
categories: 
    - 课程
    - 随机信号分析
    - 笔记
tags:
    - 随机信号分析
    - 复习笔记
---

这是复习笔记，只记录自己认为的重难点，并不全面，仅供参考。

## 概念重难点

### 随机变量的变化

> 这里会出考题，和概率论的类似，求变换后的概率密度，作业题1-22

基本做法：使用Y到X的变换关系，求导数，然后带个公式就行了。

$$x=h(y)\\
p(y)=\left|\frac{dx}{dy}\right|p(x)=\left|\frac{dx}{dy}\right|p[h(y)]$$

也有一些结论，比如两个**相互独立**的变量的和的概率分布是两个变量的概率分布的卷积（作业1-24）。

难点是多个变量的变换，需要使用雅可比行列式。
$$
p_2(y_1,y_2)=p_2(x_1,x_2)\left|\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}\right|=p_2[h_1(y_1,y_2),h_2(y_1,y_2)]\left|\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}\right|\\
\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}=\left|\begin{matrix} \frac{\partial x_1}{\partial y_1} & \frac{\partial x_1}{\partial y_2}\\ \frac{\partial x_2}{\partial y_1}&\frac{\partial x_2}{\partial y_2}\end{matrix}\right|
$$

### 随机变量/随机过程

#### 定义



## 作业题更正
