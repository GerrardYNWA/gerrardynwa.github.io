title: VINS-Mono---A Robust and Versatile Monocular Visual-Inertial State Estimator
date: 2018-10-04 21:49:48
categories: Translation

tags: [computer vision]
---

VINS-Mono的粗略翻译。。。

<!-- more -->

#### Abstract

由摄像机和低成本惯性测量单元(IMU)组成的单目视觉惯性系统(VINS)，构成了用于度量六自由度状态估计的最小传感器套件。然而，由于缺乏直接距离测量，这套系统在IMU处理、估计器初始化、外部标定和非线性优化等方面面临着诸多挑战。在本文中，我们提出了一种鲁棒的、通用的单目视觉惯性状态估计器VINS-Mono。我们的方法从一个稳健的程序开始，用于估计器初始化和故障恢复。采用一种基于紧耦合、非线性优化的方法，通过融合预计分的IMU测量数据和特征观测数据，获得高精度的视觉惯性里程计。结合我们紧耦合的公式，一个闭环检测模块能够以最小的计算开销进行重定位。除此之外，我们还对四自由度姿态图进行了优化，以加强全局一致性。我们验证了该系统在公共数据集和真实世界实验上的性能，并与其他最先进的算法进行了比较。我们还在MAV平台上执行星载闭环自主飞行，并将算法移植到基于IOS的演示中。我们强调，所提议的工作是一个可靠、完整和多功能的系统，适用于需要高精度定位的不同应用程序。我们为个人电脑和iOS移动设备开放了我们的实现方法。

#### Index Terms-

### 1. Introduction

### 2. Related Work

### 3. Overview

### 4. Measurement Preprocessing

### 5. Estimator Initialization

### 6. Tightly Coupled Monocular VIO

### 7. Relocalization

### 8. Global Pose Graph Optimization and Map Reuse

### 9. Experimental Results

### 10. Conclusion and Future Work





