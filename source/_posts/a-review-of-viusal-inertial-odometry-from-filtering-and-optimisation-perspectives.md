title: A Review of Viusal Inertial Odometry from Filtering and Optimisation
  Perspectives
date: 2018-06-30 22:59:52
categories: Translation

tags: [computer vision, slam, vio]
---

　　视觉惯性里程计（VIO）是一种利用机载相机和IMU传感器所得的测量信息，来估计移动平台的位姿随时间变化的技术。近年来，由于这两种传感器的尺寸小巧而且价格相对低廉带来的优势，VIO受到了大量研究学者的关注，并且在各种潜在的应用中得到了广泛的运用。然而，考虑到精度、实时性、鲁棒性和运行场景规模，无论是技术开发还是工程应用，VIO都是极具挑战性的。本文将从两种主流方法（滤波法和优化法）的角度来剖析当前VIO技术的研究现状。为此，本文首先对3D运动刚体的各种表示形式进行了介绍，然后分别回顾了滤波法和优化法。这两种方法之间的联系可以通过贝叶斯最大后验概率框架来阐明。除此之外，本文也会讨论一些其他的特征，譬如可观性和自标定。

<!-- more -->

​	