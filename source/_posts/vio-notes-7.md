title: VIO课程笔记（第7讲）
date: 2019-08-02 23:25:01
categories: Algorithm

tags: [computer vision, slam, vio]
---
　　[深蓝学院《从零开始手写VIO》](http://www.shenlanxueyuan.com/course/160)课程笔记——第7讲：VINS系统构建
<!-- more -->

- 

## Section 3 - VINS系统

### 1. VINS系统三大块

> 1. **前端、数据处理**：特征提取匹配、IMU积分
> 2. **初始化**：系统初始状态变量（重力方向、速度、尺度等等）
> 3. **后端**：滑动窗口优化

### 2. 后端滑动窗口优化

 VINS系统优化的状态变量为：

通过最小化滑动窗口中的残差项来估计系统的状态向量：

注意：其中鲁棒核函数$ {\rho}(·) $仅处理视觉outlier