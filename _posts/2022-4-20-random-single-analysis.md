---
title: 随机信号分析复习笔记
categories: 
    - 课程
    - 随机信号分析
    - 笔记
tags:
    - 随机信号分析
    - 复习笔记
mathjax: true
---

这是复习笔记，只记录自己认为的重难点，并不全面，仅供参考。

- this will be replaced by a toc
{:toc}

## 概念重难点

### 随机变量的变化

> 这里会出考题，和概率论的类似，求变换后的概率密度，作业题1-22

基本做法：使用Y到X的变换关系，求导数，然后带个公式就行了。
****
$$
x=h(y)\\
p(y)= \left| \frac{dx}{dy} \right| p(x)= \left| \frac{dx}{dy} \right| p[h(y)]
$$

也有一些结论，比如两个**相互独立**的变量的和的概率分布是两个变量的概率分布的卷积（作业1-24）。可以看概率论PPT《随机变量的函数及分布》，**里面有结论及推导**。

难点是多个变量的变换，需要使用雅可比行列式。（作业题1-15）~~个人感觉不会考这个部分。~~我也说不准，还是把雅可比矩阵背一下。

$$
p_2(y_1,y_2)=p_2(x_1,x_2)\left|\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}\right|=p_2[h_1(y_1,y_2),h_2(y_1,y_2)]\left|\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}\right|\\
\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}=\left|\begin{matrix} \frac{\partial x_1}{\partial y_1} & \frac{\partial x_1}{\partial y_2}\\ \frac{\partial x_2}{\partial y_1}&\frac{\partial x_2}{\partial y_2}\end{matrix}\right|
$$

### 随机过程的二维概率分布

联合分布函数

$$
F_2(x_1,x_2;t_1,t_2) = P(X_1\leq x_1,X_2\leq x_2)
$$

> **注意理解**：这里的意思是描述了 $$t_1$$ 时刻与 $$t_2$$ 时刻的时候，随机过程的相关性，即：在 $$t_1$$ 时刻取值可能会影响到 $$t_2$$ 时刻的取值，通过看这个函数就能知道具体的影响， $$x_1$$ 与 $$x_2$$ 这时候相当于是两个随机变量。
> 这里也能辅助理解后面相关函数的定义。

### 随机过程的数字特特征

#### 自相关函数——二阶混合原点矩（随机变量的混合矩）

$$
R_x(t_1,t_2) = E[X(t_1) \cdot X(t_2)]
$$

没有减去数学期望，包含了**均值和方差对相关程度的影响**

#### 协方差——混合中心距
$$
C_X(t_1,t_2)=E\{ \left[ X(t_1)-m_X(t_1) \right]\left[ X(t_2)-m_X(t_2) \right]\}
$$
减去了数学期望，反应一个随机过程在不同两个时刻的取值时间的平均关系程度。包含了离散程度对相关程度的影响

#### 自相关函数与协方差和方差的关系

当$$t_1=t_2=t$$时
$$R_X(t,t)=E[X(t)\cdot X(t)]=E[X^2(t)]$$ 是均方值。
$$C_X(t,t)=E\{[X(t)-m_X(t)]^2\}=\sigma^2_X(t)$$ 是方差。
$$\therefore \sigma^2_X(t)=E[X^2(t)]-m^2_X(t)$$

#### 相关系数——归一化协方差

$$
r_xy=\frac{C_xy}{\sigma_x \sigma_y}
$$

> 这个只看到对随机变量的定义，没看到对随机过程的。。。。

#### 随机过程两个不同时刻取样值之间的关系

1. $$p2(x_1,x_2;t_1,t_2)=p(x_1,t_1)p(x_2,t_2)$$，统计独立
2. $$R_X(t_1,t_2)=0$$，相互正交
3. $$C_X(t_1,t_2)=0$$，互不相关

> 统计独立一定互不相关，统计不独立可以不相关。独立和相关的关系在概率论中有更详细的描述。
> 互不相关在任一随机变量均值为零的时候与相互正交等价。
> 统计独立与相互正交没有关系。

#### 例题中的知识点

1. 高斯变量的概率密度由它的数学期望和方差唯一决定。
2. 当X与Y为线性关系，它们的相关系数为1，即X与Y是完全相关的。
3. 两个互相不独立的随机变量可以是不相关的。
   - 例题中举的例子是 $$\cos\phi$$ 与 $$\sin\phi$$，两个变量很显然不是统计独立的，但是他们的相关函数与协方差为$$R_{xy}=E(XY)=E(\sin\phi\cos\phi)\\C_{xy}=E[(X-m_x)(Y-m_y)]=E(XY)=0$$ 很显然二者正交且不相关。

### 随机变量/过程的特征函数

#### 定义
离散随机变量的特征函数的定义：

$$
\Phi_x(\omega)=E[e^{j\omega X}]=\sum^\infty_{k=1} [e^{j\omega x_k} \cdot p(x_k)]
$$

连续随机变量的特征函数的定义：

$$
\Phi_x(\omega)=E[e^{j\omega X}] = E(\cos \omega X+j\sin \omega X)=\int^\infty_{-\infty} e^{j\omega x} p(x) d x
$$

#### 特征函数的作用

1. 已知一个随时变量的特征函数，可以使用傅里叶变换得到其概率密度函数。
2. 可以确定随机变量经过某种变换之后的概率密度函数
    > [例题](#随机变量的概率密度作用例题)：
    > 本质上也是利用了随机变量函数的概率密度，直接套那个公式好像也是可以的。
3. 求矩函数、求高阶原点矩
    > $$
\Phi_x(\omega)=\sum_{k=0}^\infty \frac{\omega^k}{k!}\cdot\left.\frac{d^k\Phi_x(\omega)}{d\omega^k}\right|_{\omega=0}
    > $$

#### 特征函数的性质

1. $$\Phi_x(\omega)$$ 总是存在的。
2. 线性定理

    $$
    \begin{eqnarray}
    Y&=&g(X)=aX+b\\
    \Phi_Y(\omega)&=&\Phi_x(a\omega)e^{j\omega b}
    \end{eqnarray}
    $$

3. 如果随机变量 $$M_1$$ 与 $$M_2$$ 统计独立，则对于 $$Y=X_1+X_2$$ 的变换，其特征函数为

    $$
    \Phi_Y(\omega)=\Phi_1(\omega)\Phi_2(\omega)
    $$

    > 对于两相互独立的随机变量的和来说，其概率密度函数为 $$p(y)=p(x_1) \ast p(x_2)$$ ，由于概率密度与特征函数互为傅里叶变换，则该结论就很容易理解了。

4. 推论1：独立分布的随机变量之和的特征函数为各随机变量特征函数之积

    $$
    \Phi_(\omega)=\Phi_1(\omega)\Phi_2(\omega)...\Phi_n(\omega) = \prod_{k=1}^n\Phi_k(\omega)
    $$

5. 推论2：独立分布随机变量之和的概率密度函数是各自概率密度函数的卷积

    $$
    p(\omega)=p_1(x_1)\ast p_2(x_2)\ast ...\ast p_n(x_n)
    $$

> 例题 [随机变量的特征函数例题2](#随机变量的特征函数例题2)

#### 随机变量的特征函数与概率密度函数的关系

$$
p(x) = \frac{1}{2\pi} \int^\infty_{-\infty}\Phi_x(\omega)e^{-j\omega X}d \omega
$$

即，二者为傅里叶变换对

$$
p(x) \stackrel{\mathcal{F}} \longleftrightarrow \Phi_x(\omega)
$$

#### 特征函数与原点矩的关系
> 使用泰勒展开进行，具体看PPT吧。

## 作业中的重要知识点

1. 正态分布的公式一定要记清。

$$
x\sim N(m,\sigma^2)\\
p(x) = \frac{1}{\sqrt{2\pi}\sigma}\exp\left[-\frac{(x-m)^2}{2\sigma^2}\right]
$$

**注意负号**

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