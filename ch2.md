# Chapter 2: 概率理论入门

本章讲解概率和统计的一些概念。  
本书中使用概率的贝叶斯视角，但也很提到一些基础的频率统计概念。  
本章首先讨论一般的概率密度函数（PDF），然后聚焦高斯分布。  
最终，本章将介绍高斯过程，与高斯随机变量场的连续时间版本。

### 1. 概率密度函数

#### 1.1 定义

概率密度函数$p(x)$定义在x的$[a,b]$区间内，非负，且$\int_a^bp(x)dx=1$。  
*概率密度不是概率*，概率是密度函数下面的面积，即
$\text{Pr}(c\leq x\leq d)=\int_c^dp(x)dx$。

再定义条件概率密度函数$p(x|y)$和联合概率密度函数$p(x_1,x_2,\cdots,x_N)$，或
$p(\bm{x})$。

#### 1.2 贝叶斯法则和推论

联合概率密度可以分解为一个条件概率和一个非条件概率，即
$p(\bm{x,y})=p(\bm{x|y})p(\bm{y})=p(\bm{y|x})p(\bm{x})$;  
下文的$\bm{x,y}$就不加粗了，但仍然是向量哦～  
贝叶斯法则即$p(x|y)=\frac{p(y|x)p(x)}{p(y)}$  
如果我们有状态的先验$p(x)$和测量模型$p(y|x)$，则可以展开上式分母，即  
$p(x|y)=\frac{p(y|x)p(x)}{\int p(y|x)p(x)dx}$。

在贝叶斯推论中，$p(x)$称为先验，称$p(x|y)$为后验。

#### 1.3 矩

零阶矩总是1，因为概率积分为1。  
一阶矩是均值$\mu=E[x]=\int xp(x)\ dx$，其中$E[F(x)]=\int F(x)p(x)dx$是期望。  
二阶矩是协方差矩阵$\Sigma=E[(x-\mu)(x-\mu)^T]$。  
三阶矩叫skewness，四阶矩叫kurtosis，但对于多变量来说，太复杂，也无需讨论。

#### 1.4 样本均值和协方差

如果有一个PDF是$p(x)$，可以从这个密度函数中采样，记为$x_{meas}\gets p(x)$,   
可以直观地认做是这个概率密度的测量。  
可以使用样本均值和样本方差来估计分布的均值和方差，分别为：  
$\mu_{meas}=\frac{1}{N}\sum_{i=1}^Nx_{i,meas}$;  
$\Sigma_{meas}=\frac{1}{N-1}\sum_{i=1}^N(x_{i,meas}-\mu_{meas})(x_{i,meas}-\mu_{meas})^T$.  
注意方差的分母是$N-1$。

#### 1.5 统计独立与不相关

统计独立：$p(x,y)=p(x)p(y)$；  
不相关：$E[xy^T]=E[x]E[y]^T$。  
如果两个变量统计独立，则一定不相关；反之不成立。  
书中经常假设变量的统计独立性，来简化计算。

#### 1.6 归一化乘积

有时关于同一个自变量的两个PDF的乘积是有用的，归一化乘积为
$p(x)=\eta p_1(x)p_2(x)$, $\eta$是归一化常数。

对于贝叶斯，如果先验均匀分布，  
则归一化乘积可以用来融合对某个变量的多个独立的估计，即  
$p(x|y_1,y_2)=\eta p(x|y_1)p(x|y_2)$。

#### 1.7 香农和互信息

估计出PDF之后，可以用香农信息衡量确定度，即  
$H(x)=-E[\ln p(x)]=-\int p(x)\ln p(x)\ dx$  

互信息度量了知道一个变量能减少另一个变量多少不确定度，定义为  
$I(x,y)=E[\ln(\left(\frac{p(x,y)}{p(x)p(y)}\right)]=\int\int p(x,y)ln\left(\frac{p(x,y)}{p(x)p(y)}\right)dxdy$  
当$x$与$y$独立时，互信息为0。  
同时还有互信息和香农信息的关系：$I(x,y)=H(x)+H(y)-H(x,y)$。

#### 1.8 Cramer-Rao下界和Fisher信息

如果有一个确定性参数$\theta$影响随机变量ｘ的分布，可以记为$p(x|\theta)$。  
进一步假设可以从该分布中采样：$x_{meas}\gets p(x|\theta)$  
之后，Cramer-Rao下界（CRLB）认为对于该参数的给予样本的无偏估计$\hat{\theta}$
的下界是Fisher信息矩阵$I(x|\theta)$，即  
$cov(\hat{\theta}|x_{meas})=E[(\hat{\theta}-\theta)(\hat{\theta}-\theta)^T]\geq I_^{-1}(x|\theta)$  
而“无偏”表明$E[\hat{\theta}-\theta]=0$。有界表明矩阵半正定。  
Fisher信息矩阵是  
$I(x|\theta)=E[(\frac{\partial\ln p(x|\theta)}{\partial\theta})^T(\frac{\partial\ln p(x|\theta)}{\partial\theta})]$  
CRLB表明，在测量数据的基础上，对于某个参数的估计的不确定性是有下界的。  

### 2. 高斯概率密度函数

#### 2.1 定义

多元高斯分布:  
$p(x|\mu,\Sigma)=\frac{1}{\sqrt{(2\pi)^N\det\Sigma}}\exp(-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu))$  
其中均值$\mu\in\mathbb{R}^N$，协方差$\Sigma\in\mathbb{R}^{N\times N}$(对称半正定)  
高斯分布也记为$x\sim\mathcal{N}(\mu,\Sigma)$。

#### 2.2 Isserlis定理

$E[x_ix_jx_kx_l]=E[x_ix_j]E[x_kx_l]+E[x_ix_k]E[x_jx_l]+E[x_ix_l]E[x_jx_k]$  
该定理可以用来计算一些矩阵表达式，和高阶矩。

#### 2.3 联合高斯分布，以及其因素和推论

$$p(x,y)=\mathcal{N}\left(\left[\begin{array}{c}\mu_x \\ \mu_y\end{array}\right], \left[\begin{array}{cc}\Sigma_{xx} & \Sigma_{x,y} \\ \Sigma_{yx} & \Sigma_{yy}\end{array}\right]\right)$$

其中$\Sigma_{yx}=\Sigma_{xy}^T$。  
因为联合概率可以分解成条件概率和概率($p(x,y)=p(x|y)p(y)$)，我们可以得到：  
$p(x|y)=\mathcal{N}(\mu_x+\Sigma_{xy}\Sigma_{yy}^{-1}(y-\mu_y),\Sigma_{xx}-\Sigma_{xy}\Sigma_{yy}^_{-1}\Sigma_{yx})$  
$p(y)=\mathcal{N}(\mu_y,\Sigma_{yy})$

注意两个分量$p(x|y)$和$p(y)$也是高斯分布；  
并且如果通过测量知道了y，那么x的可能性也可以计算。  
这是高斯推论的基石：  
首先我们知道状态的先验$x\sim\mathcal{N}(\mu_x,\Sigma_{xx})$，  
然后可以使用测量数据$y_{emas}$来让状态分布更窄（因$\Sigma$更小）  

#### 2.4 统计独立与不相关

对于高斯分布，统计独立性与不相关是等价的，因此对高斯分布两个概念通用。

#### 2.5 变量的线性变化

对于$x\sim\mathcal{N}(\mu_x,\Sigma_{xx})$，  
而$y\in\mathbb{R}^M$与$x$是线性映射，即$y=Gx$，
其中$G\in\mathbb{R}^{M\times N}$是常数矩阵，则$y$也服从高斯分布：  
$y\sim\mathcal{N}(G\mu_x, G\Sigma_{xx}G^T)$。  

证明略过。


