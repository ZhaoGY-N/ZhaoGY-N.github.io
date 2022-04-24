---
title: "在搭建博客中遇到的问题"
categories:
    - "博客搭建"
tags:
    - "博客搭建"
    - "问题"
mathjax: true
---

* will be replaced
{:toc}

## latex无法渲染

在minimal mistake这个主题中使用的是karmdown进行md的渲染，这个是可以渲染latex的，但是需要手动添加一个mathjax的js库。

可以通过在 `_includes\head\custom.html` 中添加一个代码段，并添加对应的liquid模板条件的方式实现在YAML的头文件中添加一个mathjax:true就能实现渲染的功能。详见[GitHub issues](https://github.com/mmistakes/minimal-mistakes/issues/735)
现在这个就能渲染latex了

$$
p_2(y_1,y_2)=p_2(x_1,x_2)\left|\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}\right|=p_2[h_1(y_1,y_2),h_2(y_1,y_2)]\left|\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}\right|\\
\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}=\left|\begin{matrix} \frac{\partial x_1}{\partial y_1} & \frac{\partial x_1}{\partial y_2}\\ \frac{\partial x_2}{\partial y_1}&\frac{\partial x_2}{\partial y_2}\end{matrix}\right|
$$

## kramdown 在latex上的特殊点

kramdwon只能使用两个$$作为公式段的开头和结尾，即使是行内公式也是。同时行间公式必须要在前后各留一行空白，否则还是行内公式。

## 面包屑导航用中文会乱码

毕竟这是个beta功能，有问题很正常，我有时间去提个issue。

## 阅读时间不准

直接禁用了，本身也不是很需要这个
