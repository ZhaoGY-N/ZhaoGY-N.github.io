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

$$
\begin{gather*}
x=h(y)\\
p(y)= \left| \frac{dx}{dy} \right| p(x)= \left| \frac{dx}{dy} \right| p[h(y)]
\end{gather*}
$$

也有一些结论，比如两个**相互独立**的变量的和的概率分布是两个变量的概率分布的卷积（作业1-24）。可以看概率论PPT《随机变量的函数及分布》，**里面有结论及推导**。

难点是多个变量的变换，需要使用雅可比行列式。（作业题1-15）~~个人感觉不会考这个部分。~~我也说不准，还是把雅可比矩阵背一下。

$$
\begin{gather*}
p_2(y_1,y_2)=p_2(x_1,x_2)\left|\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}\right|=p_2[h_1(y_1,y_2),h_2(y_1,y_2)]\left|\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}\right|\\
\frac{\partial (x_1,x_2)}{\partial(y_1,y_2)}=\left|\begin{matrix}\frac{\partial x_1}{\partial y_1}\frac{\partial x_1}{\partial y_2}\\\frac{\partial x_2}{\partial y_1}\frac{\partial x_2}{\partial y_2}\end{matrix}\right|
\end{gather*}
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
r_{xy}=\frac{C_{xy}}{\sigma_x \sigma_y}
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
    \begin{gather*}
    \Phi_x(\omega)=\sum_{k=0}^\infty \frac{\omega^k}{k!}\cdot\left.\frac{d^k\Phi_x(\omega)}{d\omega^k}\right|_{\omega=0}=\sum_{k=0}^\infty\frac{(j\omega)^k}{k!} E(X^k)\\
    E(X^k)=(-j)^k\frac{d^k\Phi_x(\omega)}{d\omega^k}\left.\right|_{\omega=0}
    \end{gather*}
    > $$

    > 详细过程见PPT，神来之笔是令 $$\omega = 0$$ 。
    > 由此可得据矩函数与对应的特征函数之间的关系


#### 特征函数的性质

1. $$\Phi_x(\omega)$$ 总是存在的。
2. 线性定理

    $$
    \begin{gather*}
    Y=g(X)=aX+b\\
    \Phi_Y(\omega)=\Phi_x(a\omega)e^{j\omega b}
    \end{gather*}
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
\begin{gather*}
\Phi_{x_1x_2}(\omega_1,\omega_2)=E[e^{j\omega X_1+j\omega X_2}]=\int^\infty_{-\infty}\int^\infty_{-\infty} p_2(x_1,x_2)e^{j\omega_1 X_1+j\omega_2 X_2} dx_1 dx_2\\
p_x(x_1,x_2)=\frac{1}{2\pi}\int^\infty_{-\infty}\int^\infty_{-\infty}\Phi_{x1x_2}(\omega_1,\omega_2)e^{-j\omega_1 X_1-j\omega_2 X_2}d\omega_1 d\omega_2
\end{gather*}
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

### 各态历经性

如果平稳随机过程的均值和自相关函数具有各态历经性，则称该过程为**各态历经过程**，或者是**遍历**的

### 随机过程的自相关函数

注意一下各种周期与相加的相关函数的图像
![图片]({{ site.url }}{{ site.baseurl }}\assets\images\posts\schoolClasses\randomSingleAnalysis\Snipaste_2022-04-25_15-56-29.png)

#### 性质

$$
\begin{gather*}
R_X(t_1,t_2)=C_X(t_1,t_2)+m_X(t_1)m_X(t_2)\\
C_X(\tau)=R_X(\tau)-m^2_X\\
C_X(0)=\sigma_x^2
\end{gather*}
$$

$$
\begin{gather*}
R_X(0)=E[X^2(t)]\geq 0\\
R_X(\tau)=R_X(-\tau),C_X(\tau)=C_X(-\tau)\\
R_X(0) \geq |R_X(\tau)|
\end{gather*}
$$

若**平稳随机过程**不含周期分量，则有

$$
R_x(\infty)=\lim_{|\tau|\rightarrow\infty} R_x(\tau) = m_x^2  C_x(\infty)=0
$$

注意这样得到的数学期望会有一个正负号，两个都是合理的。

**平稳随机过程**的自相关函数的傅里叶变量是非负数

#### 判断函数是否是相关函数

1. 对称性
2. 连续性（）
3. 0处取得最大值

#### 相关系数

相关系数是归一化处理后的自相关函数

$$
r_x(\tau)=\frac{R_x(\tau)-R_x(\infty)}{R_x(0)-R_x(\infty)}=\frac{C_x(\tau)}{C_x(0)}=\frac{C_x(\tau)}{\sigma_x^2}
$$

![图片]({{site.url}}{{site.baseurl}}\assets\images\posts\schoolClasses\randomSingleAnalysis\Snipaste_2022-04-25_21-00-06.png)

#### 相关时间

**相关系数**降至5%所用的时间被称为相关时间

或者 $$ \tau_0 = \int^\infty_0 r_x(\tau)d\tau $$ ，等效为一个矩形

两种定义一般得到的值不同

> 注意这里是相关系数，是已经归一化之后的，所以矩形的高度一定是1。

### 互相关函数及其性质

#### 两个不同的随机过程之间的联合概率密度函数
{:.no_toc}
没太看懂，但是PPT只有一页，课本篇幅也不大，暂时略过

#### 两个不同的随机过程之间的矩函数

1. 互相关函数 $$ R_{XY} = E[X(t_1)Y(t_2)]=\int^\infty_{-\infty}\int^\infty_{-\infty} xyp_2(x,y;t_1,t_2)dxdy $$
2. 互协方差函数 $$ C_{XY}=E \left\{ [X(t_1)-m_X(t_1)] [Y(t_2)-m_Y(t_2)] \right\} $$
3. 互相关系数 $$ r_{XY}(t_1,t_2)=\frac{C_{XY}(t_1,t_2)}{\sqrt{\sigma_X^2\sigma_Y^2}} $$

> 取自己的 $$ t_1 $$ 再取其他的随机过程的 $$ t_2 $$

#### 两个不同的随机变量之间的关系

1. 平稳相依（严格联合平稳）： $$ P_{m+n} $$ （联合概率密度函数）不随**起点时间**变化
2. 联合平稳（广义）：
   1. $$ X(t),Y(t) $$ 各自是广义平稳过程
   2. 它们的互相关函数仅是时间间隔 $$ \tau = t_2 - t_1 $$ 的单变量随机函数，即 $$ R_{XY}(t_1,t_2) = R_{XY}(\tau)$$
   3. 则称随机过程 $$ X(t),Y(t) $$ 宽平稳相关，简称联合平稳
3. 各态历经性：当随机过程 $$ X(t),Y(t) $$ 联合平稳时，若 $ \left<X(t)Y(t)\right> \xlongequal{P} \overline{X(t)Y(t+\tau)}  $
4. 独立性： $P_{m+n}(\cdots)=P_n(\cdots)P_m(\cdots)$，统计独立
5. 不相关： $R_{XY}(\tau)=\text{常数},C_{XY}(t)=0,r_{xy}(t)=0$ ，则称为不相关
   - 判断条件：$R_{XY}=E[X(t)Y(t_\tau)]=m_Xm_y $
   - 或 $E[X(t)Y(t+\tau)]=E[X(t)]\cdot E[Y(t+\tau)] $
6. 正交性：若对于任意的 $\tau$ 都有，$R_{XY}(\tau)=0,C_{XY}(\tau)=-m_X m_Y $，则正交

#### 互相关函数的性质

1. $R_{XY}(\tau) = R_{YX}(-\tau) \quad R_{XY}(0)=R_{YX}(0) \quad C_{XY}(\tau)=C_{YX}(-\tau)$ ![图片]({{site.url}}{{site.baseurl}}\assets\images\posts\schoolClasses\randomSingleAnalysis\Snipaste_2022-04-25_23-01-38.png)
2. ![图片]({{site.url}}{{site.baseurl}}\assets\images\posts\schoolClasses\randomSingleAnalysis\Snipaste_2022-04-25_23-03-02.png)
3. ![图片]({{site.url}}{{site.baseurl}}\assets\images\posts\schoolClasses\randomSingleAnalysis\Snipaste_2022-04-25_23-05-26.png)

#### 互相关函数应用的工程实例

互相关接收器

### 平稳随机过程的功率谱密度

1. 能量信号：能量有限，持续时间有限（非周期），平均功率为零
2. 功率信号：能量趋于无穷，平均功率有限（周期性信号或随机信号）
> 一个信号可以既不是能量型信号，也不是功率型信号，但是不可能既是能量型信号又是功率型信号

#### 巴萨瓦尔定理

$$
E=\int^\infty_{-\infty}|s(t)|^2dt=\frac{1}{2\pi}\int^\infty_{-\infty}|S(\omega)|^2d\omega
$$

总能量等于各频谱分量能量之和

或者说：一个信号所含的能量（功率）恒等于此信号在完备正交函数集中各分量能量（功率）之和

#### 功率谱密度的定义

将样本信号截短，宽度为T，使其变成能量有限性信号，则可进行傅里叶变换。

经过推导可得

$$
G_X(\omega)=E\left[\lim_{T\rightarrow\infty}\frac{|X_T(\omega)|^2}{T}\right]
$$

#### **维纳-辛钦定理**

$$
R_X(\tau)\stackrel{\mathcal{F}} \longleftrightarrow G_X(\omega)
$$

自相关函数的傅里叶变换是功率谱密度。

$$
R_X(\tau)=\frac{1}{2\pi}\int_{-\infty}^\infty G_X(\omega)e^{j\omega\tau}d\omega
$$

注意一下几点问题：
1. 又傅里叶变换可知，时域信号 $R_X(\tau)$ 必须满足以下绝对可积条件

    $$
    \int^{\infty}_{-\infty}|R_x(\tau)|d\tau<\infty \quad \int^{\infty}_{-\infty}|G_x(\omega)|d\omega<\infty
    $$

2. 维纳-辛钦定理进对**平稳过程**的相关函数$R_X(\tau)$才有用
3. 功率谱密度为自相关函数的傅里叶变换，包含$R_X(\tau)$中的所有全部信息
4. 功率谱密度反应信号的频域结构，这一点与幅度谱相似，但是自功率谱密度所反应的是信号幅制的平方，因此频域结构更加明显

#### 简单求解法

利用$G_X$是一个实偶函数的特点

$$
\begin{gather*}
\left.
\begin{array}
G_X(\omega) = 2\int^\infty_0 R_x(\tau)\cos\omega\tau d\tau \\
R_x(\tau)=\frac{1}{\pi}\int^\infty_0 G_X(\omega\tau) \cos\omega\tau d\omega\\
\end{array}
\right\}\text{注意这里两个cos都是正的}\\
F_x(\omega)=2G_x(\omega)\quad \omega>0
\end{gather*}
$$

#### 联合平稳随机过程的互谱密度

![图片]({{site.url}}{{site.baseurl}}\assets\images\posts\schoolClasses\randomSingleAnalysis\Snipaste_2022-04-26_17-15-49.png)

### 复随机过程

#### 实信号的复数表示

将窄带信号的载波频率与信号通过三角函数进行分离

实信号：$s(t)=a_x(t)cos[\omega_0(t)+\phi_x(t)]$

实信号经过和差化积：$s(t)=s_I(t)\cos(\omega_0 t)-s_Q(t)\sin(\omega_0 t)$

复信号：$\tilde{s}(t)=s(t)+j\hat{s}(t)$

#### 希尔伯特变换

$$
\hat{s}(t)=s(t)\otimes\frac{1}{\pi t}=H[s(t)]
$$

公式重点记住$\frac{1}{\pi t}$

#### 数学期望

分别是实部的数学期望以及虚部的数学期望

#### 方差

$$
D[Z]=D[X]+D[Y]=E[\mathring{X^2}]-E[\mathring{Y^2}]+E[2j\mathring{X}\mathring{Y}]
$$

#### 协方差

$$
C_{Z_1 Z_2}=C_{X_1 X_2}+C_{Y_1 Y_2}+j[C_{X_1 Y_2}-C_{Y_1 X_2}]
$$

#### 相关函数

$$
\begin{gather*}
R_{X\hat{X}}(\tau)=-R_{X\hat{X}}(-\tau)\\
R_{X\hat{X}}(\tau)=R_{\hat{X}X}(-\tau)
\end{gather*}
$$

#### 功率谱密度

$$
\begin{gather*}
G_{\tilde{X}}(\omega)=\left\{ \begin{array} \text{4} G_X(\omega) \quad \omega>0 \\0 \quad \omega<0\end{array} \right.
\end{gather*}
$$

#### 窄带噪声

若白噪声（宽带）通过一个带通滤波器（窄带），且$\frac{\Delta\omega}{\omega_0}\gtrless 1$，则此噪声成为一个窄带噪声，这种窄带噪声成为窄带随机过程或窄带过程

窄带随机过程**幅值的分布**为**正态分布**

自相关函数实部与虚部相等。

![图片]({{site.url}}{{site.baseurl}}\assets\images\posts\schoolClasses\randomSingleAnalysis\Snipaste_2022-04-26_23-01-41.png)

## 作业中的重要知识点

1. 正态分布的公式一定要记清。

$$
\begin{gather*}
x\sim N(m,\sigma^2)\\
p(x) = \frac{1}{\sqrt{2\pi}\sigma}\exp\left[-\frac{(x-m)^2}{2\sigma^2}\right]
\end{gather*}
$$

**注意负号**
