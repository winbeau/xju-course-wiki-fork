# 信号分析基础

## 1 信号与系统的基本概念

---

- 信号定义：信号是信息的载体，信息是信号的内涵。
- 信号的分类：
    - 连续时间信号 - 离散时间序列
    - 周期信号 - 非周期信号
    - 确定性信号 - 随机信号
    - 能量信号 - 功率信号。能量信号绝对平方可积（和），否则称为功率信号。
    - 因果信号 - 反因果信号。**右边信号**就是**因果信号**，**左边信号**就是**反因果信号**。
- 连续与离散信号的运算：
    - 反褶
    - 移位
    - 尺度变换
    - 加、减、乘、标量乘
    - 差分运算：向前差分：$\nabla x[n] = x[n+1] - x[n]$；向后差分：$\Delta x[n] = x[n] - x[n-1]$。且 $\nabla x[n] = \Delta x[n-1]$。
    - 卷积运算：连续信号的卷积分：$\int_{-\infty}^{\infty} f_1(\tau) f_2(t-\tau) d\tau$；离散信号的卷积：$x[n] * y[n] = \sum_{k=-\infty}^{\infty} x[k] y[n-k]$。卷积运算的性质：交换律、分配律、结合律。
- 常见的信号序列：
    - 正弦类：$f(t)=A\cos(\omega t+\varphi)$。根据欧拉恒等式，正弦函数信号可以写为：$\sin(\omega t) = \frac{e^{j\omega t}-e^{-j\omega t}}{2j}$，$\cos(\omega t) = \frac{e^{j\omega t}+e^{-j\omega t}}{2}$。
    - 指数类：$f(t)=Ae^{st}$。根据欧拉等式，指数函数信号可以写为：$e^{j\omega t} = \cos(\omega t) + j\sin(\omega t)$。
    - 单位冲激信号：$\boxed{f(t)=\delta(t)=\begin{cases} \infty & t = 0\\0 & t\neq 0\end{cases}}$ 且有 $\boxed{\int_{-\infty}^{\infty} \delta(t) dt=1}$，且有如下筛选特性：$\int_{-\infty}^{\infty}f\left(t\right)\delta\left(t\right)dt=\int_{0-}^{0+}f\left(t\right)\delta\left(t\right)dt=f\left(0\right)\int_{0-}^{0+}\delta\left(t\right)dt=f\left(0\right)$
    - 单位阶跃信号：$\boxed{f(t)=u(t)=\begin{cases} 1 & t > 0\\0 & t < 0\end{cases}}$.
    - 门函数：$\boxed{\prod(\frac{t}{\tau}) = u(t+\frac{\tau}{2}) - u(t-\frac{\tau}{2}) = \begin{cases} 1 & |t| < \frac{\tau}{2} \\ 0 & others \end{cases}}$；矩形序列：$R_N(n) = \begin{cases} 1 & 0\leq n\leq N-1 \\ 0 & others \end{cases}$。
    - 内插函数信号（辛格函数）：$sinc(x) = \frac{\sin(x)}{x}$。
- 系统：
    - 直接理解成这个就行：$y(t)=T[x(t)]$
    - **连续系统与离散系统**
    - **线性系统与非线性系统**。线性系统要满足**可加性**和**比例性**，即：$T[x_1(t)+x_2(t)]=T[x_1(t)]+T[x_2(t)]$、$T[a_1x_1(t)]=a_1y_1(t)$。一般来说，带常数就不是线性系统，同时不满足比例性和可加性。
    - **时变系统与时不变系统**。时不变系统要满足 $T[x(t-t_0)]=y(t-t_0)$ 或 $T[x(n-m)]=y(n-m)$
    - 判断线性、时不变性的关键点在于，套用公式时，**要明确是对 $x(t)$ 或 $x(n)$ 进行变换（即 $T[x(t)]$ 或 $T[x(n)]$），还是对 $t$ 或 $n$ 进行变换（即 $y(t)$ 或 $y(n)$）**。
    - 同时具有**线性**和**时不变性**的系统成为**线性时不变系统**，也即 **LTI 系统**
    - **因果系统与非因果系统**。如果输出取决于**未来的输入**则成为非因果系统。非因果系统是不可物理实现的
    - **稳定系统**。输入有界且输出也有界，称为稳定系统，否则称为不稳定系统
    - **零输入响应**：**输入信号为零**，仅由**系统初始状态**(系统没有外部激励时系统的固有状态)单独作
    用于系统而产生的输出响应，用 $y_{zi}(t)$ 表示
    - **零状态响应**：忽略系统的初始状态，**只由外部激励**作用于系统而产生的输出响应，用 $y_{zs}(t)$ 表示
    - **全响应**：$y_{zi}(t) + y_{zs}(t)$
        
## 2 连续信号的傅里叶变换

---

#### Fourier 级数
![傅里叶级数的单边频谱](image.png)
![傅里叶级数的双边频谱](image1.png)


- **三角形式的傅里叶级数**：$\boxed{f\left(t\right)=a_{0}+\sum_{n=1}^{\infty}\left(a_{n}\cos n\omega_{1}t+b_{n}\sin n\omega_{1}t\right)}$；余弦形式：$f\left(t\right)=c_{0}+\sum_{n=1}^{\infty}c_{n}\cos\left(n\omega_{1}t+\varphi_{n}\right)$；正弦形式：$f\left(t\right)=d_{0}+\sum_{n=1}^{\infty}d_{n}\sin\left(n\omega_{1}t+\theta_{n}\right)$
- 直流分量：$a_{0}=\frac{1}{T_{1}}\int_{0}^{T_{1}}f\left(t\right)dt=\frac{1}{T_{1}}\int_{-\frac{T_{1}}{2}}^{\frac{T_{1}}{2}}f\left(t\right)dt$
- 余弦分量系数：$a_{n}=\frac{2}{T_{1}}\int_{0}^{T_{1}}f\left(t\right)\cos n\omega_{1}tdt=\frac{2}{T_{1}}\int_{-\frac{T_{1}}{2}}^{\frac{T_{1}}{2}}f\left(t\right)\cos n\omega_{1}tdt$
- 正弦分量系数：$b_{n}=\frac{2}{T_{1}}\int_{0}^{T_{1}}f\left(t\right)\mathrm{sin}n\omega_{1}t\mathrm{d}t=\frac{2}{T_{1}}\int_{-\frac{T_{1}}{2}}^{\frac{T_{1}}{2}}f\left(t\right)\mathrm{sin}n\omega_{1}t\mathrm{d}t$
- 各项关系，其中（$n=1,2,\cdots$）：$\begin{cases}
                & a_{0}=c_{0}=d_{0} \\
                & c_{n}=d_{n}=\sqrt{a_{n}^{2}+b_{n}^{2}} \\
                & a_{n}=c_{n}\mathrm{cos}\varphi_{n}=d_{n}\mathrm{sin}\theta_{n} \\
                & b_{n}=-c_{n}\mathrm{sin}\varphi_{n}=d_{n}\mathrm{cos}\theta_{n} \\
                & \tan\theta_{n}=\frac{a_{n}}{b_{n}} \\
                & \tan\varphi_{n}=-\frac{b_{n}}{a_{n}}
                \end{cases}$
- **复指数形式的傅里叶级数**：$\boxed{f(t)=\sum_{n=-\infty}^{\infty}F_{n}e^{jn\omega_{1}t}}$，其中 $F_{n}=\frac{1}{T_{1}}\int_{0}^{T_{1}}f\left(t\right)e^{-jn\omega_{1}t}dt=\frac{1}{T_{1}}\int_{-\frac{T_{1}}{2}}^{\frac{T_{1}}{2}}f\left(t\right)e^{-jn\omega_{1}t}dt$
- 周期信号的实质：**一个周期信号由不同频率的谐波分量所组成**。什么是*谐波*？可以简单理解为能够使用公式表达的、和谐的、规律的波形
- 傅里叶级数的频谱分为**幅度谱**和**相位谱**，分别对应幅频特性和相频特性
- **从傅里叶级数三角形式导出的单边频谱**。幅频特性：$\left|c_{n}\right|=\sqrt{a_{n}^{2}+b_{n}^{2}}$；相频特性：$\varphi_{n}=\arctan\left(\frac{-b_{n}}{a_{n}}\right)$
- **从傅里叶级数复指数形式导出的双边频谱** 幅频特性：$\left|F_{n}\right|=\left|\frac{a_{n}-jb_{n}}{2}\right|=\frac{1}{2}\sqrt{a_{n}^{2}+b_{n}^{2}}$；相频特性：$\varphi_{n}=\arctan\left(\frac{-b_{n}}{a_{n}}\right)$
- 双边频谱虽然有负频率，但负频率的出现完全是数学运算的结果，并没有任何物理意义
- 周期信号频谱的特点：离散性、谐波性、收敛性


#### FT
- 正变换：$\boxed{F\left(j\omega\right)=\mathcal{F}\left[f\left(t\right)\right]=\int_{-\infty}^{\infty}f\left(t\right)e^{-j\omega t}dt}$
- 逆变换：$\boxed{f\left(t\right)=\mathcal{F}^{-1}\left[F\left(j\omega\right)\right]=\frac{1}{2\pi}\int_{-\infty}^{\infty}F\left(j\omega\right)e^{j\omega t}d\omega}$
- 傅里叶变换是一对线性变换，它们之间存在一一对应的关系
- 傅里叶级数分析对象是**周期信号**，傅里叶变换分析对象是**非周期信号**
- 傅里叶级数频率定义域是**离散频率、谐波频率处**，傅里叶变换频率定义域是**连续频率、整个频率轴**
- 傅里叶级数函数值意义是频率分量的**数值**，傅里叶变换函数值意义是频率分量的**密度值**
- 函数存在傅里叶变换的**充分**条件：$\int_{-\infty}^{\infty}|f\left(t\right)|dt<\infty$
- 根据欧拉恒等式：$F\left(j\omega\right)=\int_{-\infty}^{\infty}f\left(t\right)e^{-j\omega t}dt=\int_{-\infty}^{\infty}f\left(t\right)\cos\left(\omega t\right)dt-j\int_{-\infty}^{\infty}f\left(t\right)\sin\left(\omega t\right)dt$
- 由上式：$\begin{cases}R\left(\omega\right)=\int_{-\infty}^{\infty}f\left(t\right)\cos\left(\omega t\right)dt \\X\left(\omega\right)=-\int_{-\infty}^{\infty}f\left(t\right)\sin\left(\omega t\right)dt & \end{cases}$
- 由上式：$\boxed{\begin{cases}|F\left(j\omega\right)|=\sqrt{R^{2}\left(\omega\right)+X^{2}\left(\omega\right)} \\ \varphi\left(\omega\right)=\arctan=\frac{X\left(\omega\right)}{R\left(\omega\right)} & \end{cases}}$
- 由上式：$|F\left(j\omega\right)|$ 是**偶函数**，$\varphi\left(\omega\right)$ 是**奇函数**
- 如果信号 $f(t)$ 的傅里叶变换 $F($j$\omega )$ 当 $\omega>\omega_\mathrm{m}$ 时均为零，则称$f(t)$是带限的，正实数 $\omega_m$ 称为信号 $f({t})$ 的带宽
- 如果信号 $f(t)$ 存在一个正实数 $T_\mathrm{m}$，当$|t|>T_\mathrm{m}$ 时，$f(t)=0$，则该信号是时限的，它对应于频域有一个时宽$T_{\mathrm{m}}$
- 带限信号在时域上是无限连续时间的，即**带限信号不能是时限**的；相应地，**时限信号必然是无限带宽的**
- 典型傅里叶变换对：    
    - 门信号：$\boxed{\Pi\left(\frac{t}{\tau}\right)\xleftrightarrow{F}\tau\sin c\left(\frac{\omega\tau}{2}\right)}$
    - 单边指数信号：$\boxed{e^{-at}u\left(t\right)\xleftrightarrow{F}\frac{1}{a+j\omega}}$
    - 双边指数信号：$\boxed{e^{-a|t|}\left(a>0\right)\xleftrightarrow{F}\frac{2a}{a^{2}+\omega^{2}}}$
    - 单位冲激信号：$\boxed{\delta (t)\xleftrightarrow{F}1}$
    - 直流信号 $f(t)=E$：$\boxed{E\xleftrightarrow{F}2\pi E\delta(\omega)}$
    - 符号函数：$sgn(t)\xleftrightarrow{F}\frac{2}{j\omega}$
    - 单位阶跃信号：$\boxed{u(t) \xleftrightarrow{F} \pi\delta(\omega)+\frac{1}{j\omega}}$
        

#### FT 的基本性质
![傅里叶变换的基本性质](image2.jpg)

#### 周期信号的 FT
- 直接使用傅里叶变换的定义的前提条件是要满足**绝对可积**，但周期信号并不满足绝对可积的条件。而引入**奇异函数**后，某些不满足绝对可积的信号也可以求傅里叶变换，所以有这一节。
- 周期信号的傅里叶变换公式：$F\left(j\omega\right)=2\pi\sum_{n=-\infty}^{\infty}F_{n}\delta\left(\omega-n\omega_{1}\right)=\omega_{1}\sum_{n=-\infty}^{\infty}F_{0}\left(jn\omega_{1}\right)\delta\left(\omega-n\omega_{1}\right)$
- 余弦函数的傅里叶变换：$\mathcal{F}\left[\cos\left(\omega_{0}t\right)\right]=\pi\left[\delta\left(\omega-\omega_{0}\right)+\delta\left(\omega+\omega_{0}\right)\right]$
- 正弦函数的傅里叶变换：$\mathcal{F}\left[\sin\left(\omega_{0}t\right)\right]=\frac{\pi}{j}\left[\delta\left(\omega-\omega_{0}\right)-\delta\left(\omega+\omega_{0}\right)\right]$
- 周期单位冲击序列的傅里叶变换：$\mathcal{F}[\delta_{\omega 1}(\omega)] = \omega_{1}\delta_{\omega 1}(\omega)$
- 周期矩形脉冲序列的傅里叶变换：$E\tau\omega_{1}\sum_{n=-\infty}^{\infty}sinc\left(\frac{n\omega_{1}\tau}{2}\right)\delta\left(\omega-n\omega_{1}\right)$；其傅里叶系数：$F_{n}=\frac{1}{T}F_{0}\left(jn\omega_{1}\right)=\frac{E\tau}{T}sinc\left(\frac{n\omega_{1}\tau}{2}\right)$


#### 抽样信号的 FT
- 时域抽样定理（奈奎斯特定理）：一个频带受限的信号 $f(t)$，要想抽样后能够不失真地还原出原信号，抽样频率必须大于 2 倍信号谱的最高频率。


## 3 连续信号的拉普拉斯变换

#### LT 的定义及收敛域
- 为什么要有拉普拉斯变换：傅里叶变换需要满足绝对可积的先决条件，为不收敛的函数乘上收敛因子后，就可以满足这一条件。而乘上收敛因子再求其傅里叶变换的过程，就可以视为拉普拉斯变换。
- 求法：$\begin{cases} F\left(s\right)=\int_{-\infty}^{\infty}f\left(t\right)e^{-st}dt \\ f\left(t\right)=\frac{1}{2\pi j}\int_{\sigma-j\infty}^{\sigma+j\infty}F\left(s\right)e^{st}ds & \end{cases}$
- 收敛域：右边信号（$\sigma > \sigma_1$）、左边信号（$\sigma < \sigma_2$）、双边信号（$\sigma_1 < \sigma < \sigma_2$）、时限信号（整个 s 平面）

![常见的变换对](3.png)

#### 单边 LT 的性质
![性质](4.png)
#### 单边 LT 的逆变换
- 查表法
- 部分分式展开法
    - 分母的所有根均为单实根：分式划开，各部查表
    - 分母的根具有共轭复根且无重复根
    - 分母仅有重根
    
#### 连续时间系统的 s 域分析
- 系统函数 $H(s)$：$H(s)=\frac{Y_{ZS}(s)}{X(s)}$，它与系统的输入和输出无关，描述了系统本身的特性。一旦系统的拓扑结构已定，它也就确定了，**它存在的条件是系统的起始状态为零，即 $y_{zi(0)=0}$**。
- 线性系统的稳定性：一个系统受某种干扰信号作用时，其所引起的系统响应在干扰消失后，会最终消失，即系统可以回到干扰作用前的状态，称系统是稳定的。
- 对于一般系统，系统稳定的充要条件是冲击响应 $h(t)$ 绝对可积。
- 系统稳定性结论：
    - 稳定：*$H(s)$ 的全部极点位于 $s$ 域的左半平面*
    - 临界稳定：*$H(s)$ 在虚轴上有 $p=0$ 的单极点或一对共轭单极点，其余极点全在 $s$ 域的左半平面*
    - 不稳定：*$H(s)$ 只要有一个极点位于 $s$ 域的右半平面，或在虚轴上有二阶或二阶以上的重极点，则系统不稳定。*
    
## 4 离散信号与系统

---

#### z 变换
- $\boxed{X\left(z\right)=\sum_{-\infty}^{\infty}x\left(n\right)z^{-n}}$，其中 $z = e^{s}$
- 级数判断敛散性的两个方法：
    - $\rho=\lim_{n\to\infty}\left|\frac{a_{n+1}}{a_{n}}\right|$
    - $\eta=\lim_{n\to\infty}\sqrt[n]{\left|a_{n}\right|}$

- z 变换的收敛域：
    - 有限长序列：$0<|z|<\infty$，但两边是否能取等号要看情况，如果求和下界小于零，则不能取无穷的等号；求和上界大于零则不能取零的等号
    - 右边序列：$|z|>\lim\limits_{n\to\infty}\sqrt[n]{|x\left(n\right)|}=R_{x1}$
    - 左边序列：$|z|<\frac{1}{\lim\limits_{n\to\infty}\sqrt[n]{\left|x\left(-n\right)\right|}}=R_{x2}$
    - 双边序列：$R_{x1}<|z|<R_{x2}$
    
![典型 z 变换](8.png)

#### z 逆变换
- 部分分式法
- 幂级数法（长除法，也就是硬除）

#### z 变换的性质与定理

- 线性：$Z\left[ax(n)+by(n)\right]=aX(z)+bY(z)\quad\left(R_1<\left|z\right|<R_2\right)$，收敛域取交集
- 位移性：$Z\left[x(n-n_0)\right]=z^{-n_0}X(z)$，收敛域只会影响 $z=0$ 和 $z=\infty$ 处
- 尺度变换：$Z[a^nx(n)]=X(\frac{z}{a})~~~(R_{x1}<\left|\frac{z}{a}\right|<R_{x2})$
- 序列线性加权：${Z}\left[nx(n)\right]=-z\frac{\mathrm{d}X\left(z\right)}{\mathrm{d}z}\quad\left(R_{x1}<\left|z\right|<R_{x2}\right)$
- 初值定理：$x(0)=\lim_{z\to\infty}X(z)$
- 终值定理：$\lim_{n\to\infty}x(n)=\lim_{z\to1}(z-1)X(z)$


## 5 离散傅里叶变换（DFT）

---

## 6 快速傅里叶变换（FFT）

---

#### 按时间抽取的基-2FFT算法

- 正常算法的时间复杂度：$N^2$
- 本算法和按频率抽取的基-2FFT算法的复杂度：$\frac{N}{2}\mathrm{log}_2N$

![按时间抽取的基-2FFT算法](5.png)

#### 按频率抽取的基-2FFT算法

![按频率抽取的基-2FFT算法](6.png)

#### 逆快速傅里叶变换（IFFT）

- $x[k]=\frac{1}{N}(\mathrm{DFT}\{X^*[m]\})^*$
- 意即：将 $X[m]$ 选取共轭，用 $FFT$ 流图计算 $DFT\{X^*[m]\}$，再取共轭并除以 $N$

## 7 数字滤波器设计

---

#### 滤波器的基本概念
- 概念 离散时间系统，输入、输出均为数字信号。可以根据需要，通过数值运算改变信号频率成分的相对比例，或者有选择性的滤除输入信号的某些频率成分
- 按功能分类![alt text](image-1.png)
- 按单位脉冲响应长度分类
    - FIR 滤波器 $H(z)=\sum_{n=0}^{N-1}h(n)z^{-n}$
    - IIR(Infinite Impulse Response) 滤波器 $H(z)=\frac{\sum_{j=0}^{M}b_{j}z^{-j}}{1+\sum_{i=1}^{N}a_{i}z^{-i}}$
- 技术指标
    - 频率响应函数：$H(e^{j\omega})=\left|H(e^{j\omega})\right|e^{j\theta(\omega)}$，则：
      - 幅频特性 $\left|H(e^{j\omega})\right|$，表示信号通过该滤波器后**各频率成分振幅衰减**情况
      - 相频特性 $\theta(\omega)$，反应各频率成分通过滤波器后**各频率成分在时间上的延时**情况
    - 理想数字滤波器
      - ![alt text](image-2.png)
      - 通带衰减(dB) $A_{\mathrm{p}}=-20\lg(1-\delta_{\mathrm{p}})$
      - 阻带衰减(dB) $A_{\mathrm{s}}=-20\lg\delta_{\mathrm{s}}$
    - 实际低通数字滤波器
      - ![alt text](image-3.png)
      - $\omega_\mathrm{p}$：通带截止频率
      - $\omega_\mathrm{s}$：阻带截止频率
      - $\delta_{\mathfrak{p}}$：通带波动
      - $\delta_{\mathrm{s}}$：阻带波动

#### 常用模拟滤波器的设计方法
- 由幅度平方函数确定。看不懂，做题碰到了再说吧。
- Butterworth 低通逼近
    - ![alt text](image-4.png)
    - $\left|H(\mathrm{j}\Omega)\right|^2=\frac{1}{1+\left(\Omega/\Omega_\mathrm{c}\right)^{2N}}$
    - 具有单调下降的幅频特性
    - 最大平坦性 $|H(\mathrm{j}\Omega)|^2$ 在 $\Omega=0 $ 点的 $1$ 到 $2N-1$ 阶导数为零
    - 3dB 不变性 不管 N 为多少，所有的特性曲线都通过 -3dB 点，或者说衰减为 3dB    
- Butterworth 模拟低通滤波器的设计步骤
    - 步骤 1：确定模拟滤波器的阶数 $N$，$N\geq\frac{\lg(\frac{10^{0.1A_s}-1}{10^{0.1A_p}-1})}{2\lg(\Omega_s/\Omega_p)}$
    - 步骤 2：确定模拟滤波器的 $3dB$ 截频 $\Omega_c$，$\frac{\Omega_\mathrm{p}}{(10^{0.1A_\mathrm{p}}-1)^{\frac{1}{2N}}}\leq\Omega_\mathrm{c}\leq\frac{\Omega_\mathrm{s}}{(10^{0.1A_\mathrm{s}}-1)^{\frac{1}{2N}}}$
    - \*步骤 3：计算模拟滤波器的系统函数极点
    - \*步骤 4：得到模拟低通滤波器的系统函数 $H_L(s)$
    - 其中，步骤 3、4，也可以通过查表法得到

#### 无限长单位脉冲响应 `IIR` 数字滤波器的设计
- 脉冲响应不变法（线性变换）
    - 对应关系：$H(s)=\sum\limits_{i=1}^{N}\frac{A}{s-p_i}$ 和 $H(z)=\sum\limits^{N}_{i=1}\frac{TA_i}{1-e^{p_iT} z^{-1}}$
    - 由上面的式子可知，求出 $A_i$ 和 $p_i$ 是写出两种式子的关键
    - 优点：时域逼近良好，线性
    - 缺点：频率响应的混叠失真，只适用于限带的模拟滤波器（**低通、带通**）
- 双线性变换法（非线性变换，$tan$ 函数）
    - 对应关系：$H\left(z\right)=H_{a}\left(s\right)|_{s=\frac{2}{T}\frac{1-z^{-1}}{1+z^{-1}}}=H_{a}\left(\frac{2}{T}\frac{1-z^{-1}}{1+z^{-1}}\right)$
    - 不用分式展开，比较友好
    - 优点：避免了混叠失真（以引入非线性为代价），能直接用于设计低通、带通、高通、带阻滤波器，保持原有的幅频性能
    - 缺点：转换前后的频率呈非线性关系（可以通过频率预畸变减轻），产生相频特性失真


## 需要关注的课后习题

#### 概表

|章节|占比|关注习题|
|---|---|---|
|一|15%|1-1、1-4、1-5、1-6|
|二|20%|2-2、2-4、2-5、2-6、2-7、2-8、2-10、2-15、2-17、2-18、2-19、2-21|
|三|0~2%|无|
|四|20%|4-1、4-3、4-6、4-12、4-13、4-14、4-16、4-17|
|五|15%|5-1、5-2、5-10、5-12|
|六|15%|6-1、6-2、6-6、6-8|
|七|13~15%|7-2、7-3、7-4、7-13、7-14|

#### 第一章

P24

- 1-1
- 1-4 判断一个序列是否是周期的
- 1-5 数模转换、求解周期
- 1-6 判断系统的线性、时不变性


#### 第二章

- 43-52 页的例题

P67

- 2-2
- 2-4
- 2-5
- 2-6 前三道题
- 2-7
- 2-8
- 2-10
- 2-15
- 2-17
- 2-18
- 2-19
- 2-21

*关注线性、移位、尺度特性

#### 第三章

考得少

#### 第四章

所有例题都要看

- 4-1 7/8 不做
- 4-3
- 4-6
- 4-12
- 4-13
- 4-14
- 4-16
- 4-17

#### 第五章（更多关注课堂上讲的内容）

P157

- 5-1 要会用公式求解有限长傅里叶变换
- 5-2
- 5-10 （1）（2）
- 5-12 （3）

#### 第六章（更多关注课堂上讲的内容）

P192

- 6-1
- 6-2
- 6-6
- 6-8

#### 第七章

主要是例题

P245

- 7-2
- 7-3
- 7-4
- 7-13
- 7-14