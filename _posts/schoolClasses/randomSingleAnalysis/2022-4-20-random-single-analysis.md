---
title: 随机信号分析复习笔记
categories: 
    - 课程
    - 随机信号分析
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

### 随机变量的特征函数

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
    > [例题](../exercises/#随机变量的特征函数例题1)：
    > 本质上也是利用了随机变量函数的概率密度，直接套那个公式好像也是可以的。
3. 求矩函数、求高阶原点矩
    > $$
    \Phi_x(\omega)=\sum_{k=0}^\infty \frac{\omega^k}{k!}\cdot\left.\frac{d^k\Phi_x(\omega)}{d\omega^k}\right|_{\omega=0}=\sum_{k=0}^\infty\frac{(j\omega)^k}{k!} E(X^k)\\
    E(X^k)=(-j)^k\frac{d^k\Phi_x(\omega)}{d\omega^k}\left.\right|_{\omega=0}
    > $$

    > 详细过程见PPT，神来之笔是令 $$\omega = 0$$ 。
    > 由此可得据矩函数与对应的特征函数之间的关系


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

    > 例题 [随机变量的特征函数例题2](../exercises/#随机变量的特征函数例题2)

#### 随机变量的特征函数与概率密度函数的关系

$$
p(x) = \frac{1}{2\pi} \int^\infty_{-\infty}\Phi_x(\omega)e^{-j\omega X}d \omega
$$

即，二者为傅里叶变换对

$$
p(x) \stackrel{\mathcal{F}} \longleftrightarrow \Phi_x(\omega)
$$

#### 多维特征函数

$$
\Phi_{x_1x_2}(\omega_1,\omega_2)=E[e^{j\omega X_1+j\omega X_2}]=\int^\infty_{-\infty}\int^\infty_{-\infty} p_2(x_1,x_2)e^{j\omega_1 X_1+j\omega_2 X_2} dx_1 dx_2\\
p_x(x_1,x_2)=\frac{1}{2\pi}\int^\infty_{-\infty}\int^\infty_{-\infty}\Phi_{x1x_2}(\omega_1,\omega_2)e^{-j\omega_1 X_1-j\omega_2 X_2}d\omega_1 d\omega_2
$$

#### 多维特征函数的性质

1. 随机变量 $$X_1$$ 和 $$X_2$$统计独立的充分必要条件为： $$\Phi_{x_1,x_2}(\omega_1,\omega_2) = \Phi_{x_1}(\omega_1)\Phi_{x_2}(\omega_2)$$
2. 二维特征函数在 $$(\omega_1,\omega_2)$$ 二维实平面上一致连续
3. 二维特征函数包含了一维特征函数的信息
   > $$
\Phi_{x_1}(\omega_1) = \Phi_{x_1x_2}(\omega_1,0)
\Phi_{x_2}(\omega_2) = \Phi_{x_1x_2}(0,\omega_2)
   > $$

#### N维随机变量的特征函数

![N维变量的特征函数]({{ site.url }}{{ site.baseurl }}\assets\images\posts\schoolClasses\randomSingleAnalysis\Snipaste_2022-04-24_15-12-25.png)

### 随机过程的特征函数

和随机变量相比只是在函数中增加了一个t，计算过程以及性质都是一样的，不在赘述。

#### 随机过程的二维特征函数

和二维随机变量的特征函数类似，详见图。
![图片]({{ site.url }}{{ site.baseurl }}\assets\images\posts\schoolClasses\randomSingleAnalysis\Snipaste_2022-04-24_15-20-55.png)

**将二维特征函数对变量 $$\omega$$ 求偏导 $$n$$ 次，可得 $$n$$ 阶*混合原点*矩函数**

**则其自相关函数为**

$$
R_x(t_1,t_2)=\int^\infty_{-\infty}\int^\infty_{-\infty}x_1 x_2 p_2(x_1,x_2;t_1,t_2)dx_1 dx_2 = -\frac{\partial^2\Phi(\omega_1,\omega_2;t_1,t_2)}{\partial\omega_1\partial\omega_2}\left.\right|_{\omega_1\omega-2=0}
$$

### 随机过程的平稳性

#### 特点

统计特性（概率，矩）不随时间的平移而变化

#### 分类

1. 狭义平稳随机过程（严格平稳）：任意n维概率分布不随时间的平移而变化
   - 由同分布的随机变量组成
2. 广义平稳：矩函数不随时间的平移而变化，数学期望 $$E[X(t)]=m_X=C$$ 不随时间发生变化，自相关函数 $$R_X(t_1,t_2)=R_X(\tau)$$ 只与时间间隔相关。
   - 可以用矩的方法判断广义平稳，严格平稳则必须使用概率密度判断
   - 严格平稳必定为广义平稳，反之未必成立
   - 对于正态过程，广义平稳一定严格平稳（其分布只与均值和方差有关）

#### 说明

1. 平稳性是随机信号的随机特性对于参量（组）的移动不变性，即平稳随机信号的测试不受观察时刻的影响
2. 应用于研究最多的平稳信号是广义平稳信号
3. 严格平稳信号因要求太“苛刻”，更多的用于理论研究之中
4. 经验判据：如果产生于影响随机信号的主要物理条件不改变，那么通常可以认为此信号是平稳的
5. 非平稳信号：在较短的时间段内可以认为是一个平稳信号

#### 性质

- 彼此统计独立的平稳随机过程，它们乘积的均值和自相关函数等于各个随机过程的均值和自相关函数的乘积，所以广义平稳过程的成绩也是广义平稳过程。
- 平稳周期性随机过程的自相关函数也满足周期性。


## 作业中的重要知识点

1. 正态分布的公式一定要记清。

$$
x\sim N(m,\sigma^2)\\
p(x) = \frac{1}{\sqrt{2\pi}\sigma}\exp\left[-\frac{(x-m)^2}{2\sigma^2}\right]
$$

**注意负号**
