---
title: 随机信号分析例题习题
categories: 
    - 课程
    - 随机信号分析
tags: 
    - 随机信号分析
    - 习题
mathjax: true
---

- this will be replaced by a toc
{:toc}

## 作业题更正

### 作业P11 题2-2
不是很能理解，暂时先放弃，后面再来看吧。
![题图]({{ site.url }}{{ site.baseurl }}/assets/images/posts/2022-04-20/Snipaste_2022-04-21_21-05-13.png)

## PPT例题

### 随机变量的特征函数例题1
例题：随机变量 $$X$$ 均匀分布于 $$\left( -\frac{\pi}{2},\frac{\pi}{2}\right) $$ 上。其非线性变换关系为$$Y=\sin X$$，求$$p(y)$$

答：Y 的特征函数为

$$
\Phi_y(\omega)=E[e^{j\omega Y}]=\int^\infty_{-\infty} e^{j\omega \sin x}p(x)dx
$$

将 $$dx$$ 替换为 $$dy$$ 。

$$
dx=d(\arcsin y)=\frac{1}{\sqrt{1-y^2}}dy
$$

将 $$p(x)$$ 和 $$dx$$ 带入可得

$$
\Phi_y(\omega)=\int^1_{-1} e^{j \omega y} \frac{1}{\pi\sqrt{1-y^2}}dy
$$

利用特征函数和概率密度的关系可得

$$
p(y)=\frac{1}{\pi\sqrt{q-y^2}}
$$

### 随机变量的特征函数例题2

独立分布随机变量 $$X_1,X_2,\dots ,X_n$$ 服从高斯分布，其均值为零，方差为 $$\sigma^2_x$$ ，样本 $$X_k$$ 平均值为 $$\bar X = \frac{1}{n} \sum^n_{k=1} X_k$$ ，求 $$p(\bar x)$$

答：如果使用相加的概率密度分布的关系的话，只能处理两个，多个的卷积不容易找到规律，所以使用**特征函数**将卷积转换为相乘，这样就能找到规律了。

先求 $$X$$ 的特征函数

$$
\Phi_{x_k}(\omega) = \int_{-\infty}^\infty \exp{\left(j\omega x_k\right)} \frac{1}{\sqrt{2\pi}\sigma_x} \exp{\left(-\frac{x_k^2}{2\sigma_x^2}\right)}= exp \left(-\frac{\omega^2\sigma_x^2}{2}\right)
$$

> 积分的过程首先是将常数提出去，然后将指数函数中的平方相配成完全平方，把配出来的一项继续提出来，然后进行代换，可以得到如下式子

> $$
\Phi_{x_k}(\omega) = \frac{\exp{\left(-\frac{\omega^2\sigma^2_x}{2}\right)}}{\sqrt{\pi}}\int_{-\infty}^\infty e^{-u^2} du
> $$

> 这里有一个超越函数的积分，即

> $$
I = \int_{-\infty}^{\infty} e^{-u^2}du
> $$

> 这个积分不能使用分步积分计算（**具体原因我也不太清楚，反正不行，结果是错的**），简单的办法可以使用正态分布的概率密度积分为1进行反推，也可以转化到极坐标系下进行，具体可以看知乎这篇文章[《∫e^(-x^2)dx的三种方法》](https://zhuanlan.zhihu.com/p/146348325)。

令 $$Y = \sum_{k=1}^{n} X_k$$ ，由特征函数的性质可得

$$
\Phi_y(\omega) = \prod_{k=1}^n \Phi_{x_k}(\omega)=\exp{\left(-\frac{n\omega^2\sigma_x^2}{2}\right)}
$$

又因为

$$
\bar{X} = \frac{1}{n} \sum_{k=1}^{n} X_k = \frac{1}{n} Y
$$

使用特征函数的线性定理可得

$$
\Phi_{\bar{x}} = \exp{\left(-\frac{\omega^2\sigma^2_x}{2n}\right)}
$$

则根据第一步得到的正态分布的特征函数可以得到
1. $$\bar{X}$$ 仍为正态分布，由此可得对应的
2. 均值为0
3. 方差为 $$\frac{\sigma_x^2}{n}$$

> 这一结论与直接使用概率论的相关结论是一致的。
> $$
\begin{eqnarray}
D\left(\bar{X}\right)&=&D\left(\frac{1}{n}\sum_{i=1}^n X_i\right)\\
&=&\frac{1}{n^2}\sum_{i=1}^n D(X_i)=\frac{1}{n^2}\sum_{i=1}^n \sigma^2 = \frac{1}{n} \sigma^2\\
D\left(\bar{X}\right)&=&\frac{1}{n}\sigma^2\\
\end{eqnarray}
> $$