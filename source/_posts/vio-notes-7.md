title: VIO课程笔记（第7讲）
date: 2019-08-02 23:25:01
categories: Algorithm

tags: [computer vision, slam, vio]
---
　　[深蓝学院《从零开始手写VIO》](http://www.shenlanxueyuan.com/course/160)课程笔记——第7讲：VINS系统构建
<!-- more -->

## Section 1 - VIO相关知识回顾

### 1. IMU预积分

#### IMU传感器模型

> - $$ \tilde{\omega}^{b} = {\omega}^{b} + b^g + n^g $$
> - $$ \tilde{a}^{b} = q_{b\omega}(a^{\omega} - g^{\omega}) + b^a + n^a $$
> - g的正负在不同的论文会有不同的定义
> - 将一段时间内的IMU数据直接积分起来就能得到两时刻$ i $和$ j $之间关于IMU的测量约束，即预积分量$${\alpha}_{b_i b_j}$$、$${\beta}_{b_i b_j}$$、$${q}_{b_i b_j}$$
> - 协方差传递

### 2. 视觉几何基础

#### 视觉技术

> 1. 已知两图像：特征点提取(fast)、匹配(光流、特征描述子)
> 2. 已知两图像特征匹配点：利用对极几何约束(E矩阵、H矩阵)，计算两图像之间的pose(update to scale)
> 3. 已知相机pose和已知特征点二维坐标：通过三角化得到三维坐标
> 4. 已知3D点、2D特征点：通过Perspective-n-Point(PnP)求取新的相机pose

### 3. 问题

> 1. IMU怎么和世界坐标系对齐，计算初始时刻的$ q_{\omega b_0}$
> 2. 单目视觉姿态如何和IMU轨迹对齐，尺度如何获取
> 3. VIO系统的初始速度$ v $，传感器bias等如何估计？
> 4. IMU和相机之间的外参数等...

## Section 2 - VINS鲁棒初始化

### 1. 视觉和IMU之间的联系

#### 几何约束

> - 考虑相机坐标系

### 2. 视觉IMU对齐流程

#### 估计流程

> 1. 旋转外参数$ q_{bc} $未知，则先估计旋转外参数（IMU和相机通常离的比较近，平移不那么重要）
> 2. 利用旋转约束来估计陀螺仪bias
> 3. 利用平移约束估计重力方向、速度以及尺度初始值
> 4. 对重力向量$ g^{c_0} $进行进一步优化
> 5. 求解世界坐标系$ \omega $和厨师相机坐标系$ c_0 $之间的旋转矩阵$ q_{\omega c_0} $，并将轨迹对其到世界坐标系

#### A. 利用旋转约束估计外参数旋转$ q_{bc} $

#### B. 基于旋转约束的陀螺仪(Gyroscope)Bias

- 如果外参数已经标定好，利用旋转约束，可估计陀螺仪bias

#### C. 初始化速度、重力和尺度因子

- 需要估计的变量
- 预积分量约束

#### D. 优化重力向量$ g^{c_0} $

- 为什么需要优化重力向量？利用
- 重力向量参数化 

#### E. 将相机坐标系对齐世界坐标系(对齐流程)

1. 找到$ c_0 $到$ \omega $系的旋转矩阵$ R_{\omega c_0} = exp([{\theta}{u}]) $把所有$ c_0 $坐标系下的变量旋转到$ \omega $下
2. 把相机平移和特征点尺度恢复到米制单位
3. 至此，完成了系统初始化过程

### 3. VINS初始化拓展

#### A. 疑问

- 加速度bias为何没有估计？（相比重力，bias非常小）
- 平移外参数$ p_{bc} $为何没有初始化？（影响不太大，因为旋转很重要，平移是线性的，相对没那么重要；另外，两个相机之间平移量是很小的）

#### B. 其他初始化方法

- 静止初始化：直接用加速度测量重力方向，初始速度为0
- 除VINS-Mono外的其他运动初始化方案（两种初始化方案）

## Section 3 - VINS系统

### 1. VINS系统三大块

> 1. **前端、数据处理**：特征提取匹配、IMU积分
> 2. **初始化**：系统初始状态变量（重力方向、速度、尺度等等）
> 3. **后端**：滑动窗口优化

### 2. 后端滑动窗口优化

> - VINS系统优化的状态变量为：
> - 通过最小化滑动窗口中的残差项来估计系统的状态向量：
> - 注意：其中鲁棒核函数$ {\rho}(·) $仅处理视觉outlier