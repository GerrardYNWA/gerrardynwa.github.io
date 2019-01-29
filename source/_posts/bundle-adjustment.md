title: Bundle Adjustment
date: 2016-01-12 21:15:59
categories: Algorithm
tags: [computer vision]
---

　　机器人导航中，2D的特征reproject回三维域内，和真正的3D点的位置会有偏差。但是在物理意义上，3D点和投射到摄像机的2D特征点是同一个点。所以这个误差出现在计算3D点时摄像机自身旋转矩阵和位移向量上。Bundle Adjustment的作用是，通过least square等算法，去最小化这个偏差，以此得到机器人移动和方向的精确值。这在物理意义上是最精确的，是Visual SLAM问题的state-of-art解决方法。[`1`][1]

<!--more-->

　　其实least square problem一般都是用Gauss-Newton法或者LM算法迭代求解。bundle adjustment本质也是lm算法。由于是特定的形式，所以可以化成sparse　matrix的形式，这样计算量大大减小了。[`2`][2]

　　Gauss-Newton法想必都很清楚，这里只简述下LM算法。LM算法全称Levenberg-Marquardt算法，是最优化算法中的一种，即寻找使得函数值最小的参数向量。它是使用最广泛的非线性最小二乘算法。它是利用梯度求最大（小）值的算法，形象的说，属于“爬山”法的一种。它同时具有梯度法和牛顿法的优点。当λ很小时，步长等于牛顿法步长，当λ很大时，步长约等于梯度下降法的步长。

[1]:https://www.zhihu.com/question/29082659/answer/43132553
[2]:https://www.zhihu.com/question/29082659/answer/43138062

