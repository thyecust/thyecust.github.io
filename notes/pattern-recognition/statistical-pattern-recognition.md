# Statistical Pattern Recognition

## Bayes Method

问题背景

* 有两个分类 $\omega_1$ 和 $\omega_2$ 
* 先验概率为 $P(\omega_1)=1/3,\ P(\omega_2)=2/3$ 
* 有一组特征 $x=[x_1,x_2,...,x_d]^T$
* 对每个特征有类条件概率密度函数 $p(x|\omega_1),\ p(x|\omega_2)$

### 最小错误率贝叶斯决策

$$
P(\omega_i|x)=\frac{p(x|\omega_i)P(\omega_i)}{
\sum_{j=1}^2 p(x|\omega_j)P(\omega_j)
}, \ i=1,2
$$

* 若 $P(\omega_1|x)>P(\omega_2|x)$，则样本 x 分类为 $\omega_1$

### 最小风险贝叶斯决策

* 决策空间，$A=[\alpha_1,\alpha_2,...,\alpha_a]^T$
* 风险函数，$\lambda(\alpha_i,\omega_j), \ i=1,2,...,a,\ j=1,2$

以风险最小为判断依据
$$
R(\alpha_i|x)=\mathbb E_{j}(\lambda(\alpha_i,\omega_j))=\sum_{j=1}^2
\lambda(\alpha_i,\omega_j)P(\omega_j|x)
$$

* 最小错误率贝叶斯决策，是风险函数为常数的特例

## Linear Classifier

### 感知机

输入 $x^p=[x_1,x_2,...,x_p]$，输出 $y\in\{0,1\}$
$$
u_k=\sum_{j=0}^pw_{kj}x_j,\ y_k=\phi(u_k)
$$
其中 $x_0=1,w_{k0}=-\theta_k$ 是阈值项，$\phi(·)$ 是激活函数。

### 感知机学习

更新公式
$$
\Delta w_{ij}=\eta(t_i^p-y_i^p)·x_j^p
$$
其中 $\eta\in(0,1)$ ，是学习率，学习率越大收敛越快，学习过程越不稳定。

## K-Nearest Neighbors

缺点：

* 不相关变量
* 尺度

## Clustering

### K-means 聚类

### FCM 聚类

有 n 个样本，分到 c 个类中，加权参数 $m\ge1$。

隶属度
$$
\sum_{j=1}^c \mu_{ij}=1\\
\mu_{ik}=[\sum_{j=1}^c(\frac{d_{ik}}{d_{ij}})^{2/(m-1)}]^{-1}
$$
聚类中心
$$
v_k=\frac{\sum_{i=1}^n}{}
$$


目标函数
$$
J_b
$$
