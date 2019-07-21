title: VIO课程笔记（第1讲）
date: 2019-06-15 22:50:53
categories: Algorithm

tags: [computer vision, slam]
---
　　[深蓝学院《从零开始手写VIO》](http://www.shenlanxueyuan.com/course/160)课程笔记——第1讲：概述与课程介绍
<!-- more -->
## Section 1 - 课程内容与提要

### 重点内容

- IMU的工作原理和噪声方程
- 视觉与IMU紧耦合的基础理论
- 从零开始实现VIO紧耦合优化器（仅基于Eigen）

## Section 2 - VIO概述

### 1. VIO（IMU + Visual Odometry）

### 2. IMU与视觉定位方案优势与劣势对比

### 3. 松耦合/紧耦合（为什么要使用紧耦合？）

### 4. 探讨的问题

1. IMU的测量数据表达了系统的什么状态，受到哪些噪声影响？
2. 如何建立一个带有IMU测量信息的视觉特征点信息的非线性优化问题并求解？
3. 该问题随着时间将发生怎样的演变？

## Section 3 - 预备知识回顾

### 1. 三维刚体运动

- 坐标系（世界坐标系/IMU坐标系/相机坐标系）

### 2. 四元数

- 1实部 + 3虚部
- 四元数运算
- 单位四元数->任意旋转（角轴）
- 四元数q vs 时间导数
- 李代数->旋转求导
- 旋转矩阵R vs 时间导数

### 3. so(3)导数

- 旋转点的左扰动雅可比
- 旋转点的右扰动雅可比
- 旋转连乘的雅可比
- SO(3)的伴随性质

### 4. SE(3)李代数

## 习题

### 1. VIO文献阅读

- 视觉与IMU进行融合之后有何优势？
- 有哪些常见的视觉+IMU融合方案？有没有工业界应用的例子？
- 在学术界，VIO研究有哪些新进展？有没有将学习方法用到VIO中的例子？

### 2. 四元数和李代数更新

- R / q 更新
- 重投影（R） vs 旋转连乘（q）

### 3. 右乘so(3)