# 多元函数微分学

[toc]

## 多元函数

### 点集的基本概念

$E$ 是一个点集，如果存在 $r>0$ 使 $E\sub N(O,r)$ 那么 $E$ 是一个**有界集**，否则是**无界集**。

$E$ 是一个点集，$M$ 是一个点，如果 $\forall \delta>0$ 以下两个

* $N(M,\delta)\cap E\ne\varnothing$
* $N(M,\delta)\cap E^c\ne \varnothing$

那么 $M$ 是 $E$ 的一个**边界点**。边界点的集合称作**边界** $\part E$。

如果 $E$ 上所有的点都是内点，那么 $E$ 是一个**开集**，连通的非空开集称为**开区域**。

如果 $E$ 是开区域，那么 $\bar E=E\cup\part E$ 是一个**闭区域**。

### 多元函数的极限

以下规则对多元函数的极限仍然成立

* 四则运算和复合函数的极限运算
* 极限和无穷小
* 保序性，保号性，夹逼准则
* 极限存在 --> 局部有界

以下规则不再成立

* 单调有界准则
* 洛必达法则

### 多元函数的连续性

若多元函数 $f$ 在 $X_0$ 有定义，有极限，且定义与极限相等，那么 $f$ 在 $X_0$ 连续。

多元初等函数在定义域内是连续的。

最值定理：若多元函数 $f$ 在有界闭区域 $D$ 上连续，那么 $f$ 在 $D$ 上有最大值、最小值。

介值定理：若多元函数 $f$ 在有界闭区域 $D$ 上连续， $f$ 在 $D$ 上有最大值 $M$、最小值 $m$，那么 $\forall m<\mu<M,\ \exist \xi\in D,\ f(\xi)=\mu$。

## 偏导数

### 全微分

如果函数 $f(x,y)$ 在 $(x,y)$ 处的全增量可以表示成
$$
f(x+\Delta x,y+\Delta y)-f(x,y)=A\Delta x+B\Delta y+o(\sqrt{x^2+y^2})
$$
那么 $f$ 在 $(x,y)$ **可微**，$A\Delta x+B\Delta y$ 是 $f$ 在 $(x,y)$ 的**全微分**。

* 可微必可偏导，$f_x(x,y)=A,f_y(x,y)=B$
* 可偏导未必可微，如 $f(x,y)=(xy)/(x^2+y^2)$
* 可微必连续
* 可偏导且偏导连续，必可微

### 方向导数

方向导数描述了
$$
\lim_{P\rightarrow P'}\frac{f(P)-f(P')}{|\vec{PP'}|}
$$
若 $\vec l$ 的方向角是 $\alpha,\beta,\gamma$，$f$ 在 $P$ 可微，那么 $f$ 在这一点对 $\vec l$ 的导数存在
$$
\frac{\part f}{\part \vec l}=\frac{\part f}{\part x}\cos\alpha
+\frac{\part f}{\part y}\cos\beta
+\frac{\part f}{\part z}\cos\gamma=\nabla f\cdot (\cos \alpha,\cos \beta,cos \gamma)
$$
可以表示成梯度的投影。

## 隐函数微分

已知
$$
\begin{cases}
F(x_1,x_2,\cdots,x_n,u,v)=0\\G(x_1,x_2,\cdots,x_n,u,v)=0
\end{cases}
$$
确定 $u(x_1,x_2,\cdots,x_n)$ 和 $v(x_1,x_2,\cdots,x_n)$ 。
$$
\frac{\part u}{\part x_i}=-\frac{\frac{\part (F,G)}{\part (x_i,v)}}{\frac{\part (F,G)}{\part (u,v)}}
$$

## 几何应用

### 曲线

已知平面光滑曲线 $F(x,y)=0$，有

* 切线，$F_x(x_0,y_0)(x-x_0)+F_y(x_0,y_0)(y-y_0)=0$
* 法线，$F_y(x_0,y_0)(x-x_0)-F_x(x_0,y_0)(y-y_0)=0$

已知空间曲线 $x=\phi(t),y=\psi(t),z=\omega(t)$

* 切向量 $(\phi',\psi',\omega')$

已知空间曲线 $F(x,y,z)=0,G(x,y,z)=0$

* 切向量是 $\nabla F\times\nabla G$

$$
\left|
\begin{matrix}
\vec i & \vec j & \vec k \\
F_x    & F_y    & F_z    \\
G_x    & G_y    & G_z
\end{matrix}
\right|
$$

### 曲面

已知光滑曲面 $F(P)=0$ ，那么在 $P_0$ 处

* 法向量 $\vec n=(F_x(P_0),F_y(P_0),F_z(P_0))$
* 切平面 $n_x(x-x_0)+n_y(y-y_0)+n_z(z-z_0)=0$

如果已知光滑曲面 $z=f(x,y)$ 那么

* 法向量 $\vec n=(-f_x,-f_y,1)$

## 高阶偏导数

## 多元函数的极值和最值

如果 $P$ 满足 $\nabla f(P)=0$，那么 $P$ 是 $f$ 的**稳定点/驻点**。稳定点与偏导数不存在的点合成**临界点**，极值点一定是临界点。不是极值点的临界点称为**鞍点**。

设 $f$ 在 $N(P,\delta)$ 内有二阶连续偏导，记
$$
H=\left|\begin{array}{xx}
f_{xx}(P) & f_{xy}(P) \\
f_{yx}(P) & f_{yy}(P)
\end{array}\right|
$$
那么

* $H>0$，$f_{xx}(P)>0$，$P$ 是极小值点
* $H>0$，$f_{xx}(P)<0$，$P$ 是极小值点
* $H<0$，$P$ 是鞍点
* $H=0$，没有结论

### 拉格朗日乘数法

在 $\phi(x,y)=0$ 下，求 $f(x,y)$ 的极值，相当于求 $f(x,\psi(x))$ 的极值，有
$$
\frac{\mathrm{d}f(x,y)}{\mathrm{d}x}=f_x+f_y\frac{\mathrm{d}y}{\mathrm{d}x}=0
$$
注意到
$$
\frac{\mathrm{d}y}{\mathrm{d}x}=-\frac{\phi_x}{\phi_y}
$$
所以
$$
\begin{cases}
f_x+\lambda\phi_x=0\\
f_y+\lambda\phi_y=0\\
\phi(x,y)=0
\end{cases}
$$
我们定义拉格朗日函数 $F(x,y)=f(x,y)+\lambda\phi(x,y)$，那么极值点满足 $F_x=F_y=F_\lambda=0$ 。