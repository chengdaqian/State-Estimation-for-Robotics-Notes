# Chapter 1: 简介

本书将首先介绍一些经典的估计方法，可用于线性高斯系统；  
然后将介绍一些像非线性系统与非高斯噪声的扩展方法；  
还会开个小差，介绍如何讲状态估计结果用于在三维世界中操控机器人，提倡一种处理
旋转的方式：李群。

### 1. 历史

四千年前，航海者需要进行状态估计。  
到十五世纪，发明了海事罗盘和航海图，可以在海上进行状态估计。  
后来发明了一系列其他的测量红菊，如使用天体导航测量纬度；  
而测量经度则是依靠便携钟表的发明。

天文学中也有状态估计。  
高斯发明了最小二乘，用以在预测轨道时最小化测量误差的影响；  
其后，他证明了在误差高斯分布下，最小二乘最优。

在二十世纪中叶，估计问题开始发展，这与计算机的发明相关。  
1960年卡尔曼发表了两篇里程碑论文，定义了很多之后状态估计领域的内容：  
他首先定义了可观测性，即动态系统中的一个状态是否可以通过测量数据中来推测；  
他又定义了噪声存在下，估计系统状态的最佳框架，即卡尔曼滤波器，流行了五十年。  
NASA最先使用KF来帮助航天器进行状态估计。

十五年前（两千年左右），状态估计这个研究领域开始衰落，  
但随着新的传感器技术，这个领域开始迎接新的挑战。

### 2. 传感器，测量，和问题定义

传感器精度有限，因而测量数据有不确定性。  
估计状态时，需要记录不确定性，从而知道我们对估计结果的自信程度。  
*状态估计是为了用不完美的传感器获得最好的估计。*  
但同时我们也力求提高传感器。  
传感器分两类：内感受的（interoceptive）和外感受的（exteroceptive）。  
前者包括加速度计、陀螺仪、轮子里程计（测量角速度）；  
后者包括相机、TOF发射接收器（如激光测距仪、GPS）。  
一般来讲，前者测量速度、加速度，后者测量位置和姿态。  
最好的状态估计同时使用这两种传感器，如GPS加IMU，  
再如现在卫星使用探测太阳、星体的传感器和三自由度陀螺仪来估计状态。

**问题定义:   
Estimation is the problem of reconstructing the underlying state of a system
given a sequence of measurements as well as a prior model of the system.  
估计问题是给定一系列测量数据与系统的先验模型，来重建系统的状态。**

状态估计问题和方案都有很多，目标是理解在哪种情况下应该用哪种方法。

### 3. 本书架构

本书由三部分组成：  
1. 估计机器（Estimation Machinery）
2. 三维机器（Three-Dimensional Machinery）
3. 应用（Applications）

第一部分讲解了经典和state-of-the-art的估计工具，但先不处理三维的事情，
状态假设为一个一般的向量；  
内容包含了递归状态估计方法和批方法（batch methods），都是基于贝叶斯方法；  
对比了贝叶斯方法和最大后验（MAP）方法，并讲解两者对非线性问题的区别；  
书中还讲连续时间估计与机器学习中的高斯过程回归相结合；  
最终讨论了一些实际问题，如鲁棒估计和biases。  


第二部分讲解了基础的三维几何，并对矩阵李群做了详细介绍；  
旋转并不是通常意义的向量，因此第一部分的估计方法不能直接适用；  
因此，第二部分详述了几何、运动学、旋转和位姿的概率/统计。

第三部分结合了前两部分，讲述了一系列经典三维估计问题；  
提供了一系列易于实现的方法。

### 4. 与其他书的关系

*Probabilistic Robotics (2006, Thrun)* 专注于概率的状态估计方法，但针对二维世界；  
方法可以扩展至三维世界，但并没有讲述。

*Computational Principles of Mobile Robotics (2010, Dudek)* 讲述了移动机器人
与状态估计,包括定位和建图方法，但没讲三维。

*Mobile Robotics: Mathematics, Models, and Methods (2013, Kelly)* 讲述了移动
机器人和状态估计，包括三维情况，但因为该书诺括了机器人学的方方面面，并没有深
入讲解如何处理三维状态估计中的旋转变量。

*Robotics, Vision, and Control (2011, Corke)* 非常全面，但并不深入讲解状态估
计。
*Bayesian Filtering and Smoothing (2013, Sarkka)* 深入讲解了递归方法；  
并不讲解批方法，也不讲解三维估计。


*Stochastic Models, Information Theory, and Lie Groups: Classical Results 
and Geometric Methods (2009, Chirikjian)* 讲解了使用矩阵李群做状态估
计，比较理论，讲解了机器人以外的应用。


*Engineering Applications of Noncommutative Harmonic Analysis: With 
Emphasis on Rotation and Motion Groups (2001, Chirikjian)* 与最新的更新 
*Harmonic Analysis for Engineers and Applied Scientists: Updated and 
Expanded Edition (2016)* 讲解了使用李群表现概率分布。在本书中，我们只讲解
近似的方法，适用于旋转不确定性不大的情况。

* Optimization on Matrix Manifolds (2009, Absil)*  不讲解状态估计，但讲解了
如何处理优化目标并非向量时的优化问题，因为旋转并不像向量，因此与机器人相关。


