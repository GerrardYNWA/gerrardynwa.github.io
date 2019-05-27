title: The History of Bundle Adjustment
date: 2016-08-06 11:46:43
categories: Algorithm
tags: [computer vision]
---

　　转载自知乎versatran01的回答：[Bundle Adjustment到底是什么？](https://www.zhihu.com/question/29082659/answer/62472382)

<!--more-->

---

　　Adjustment computation最早是由geodesy的人搞出来的。19世纪中期的时候，geodetics的学者就开始研究large scale triangulations了。20世纪中期，随着camera和computer的出现，photogrammetry也开始研究adjustment computation，所以他们给起了个名字叫bundle adjustment，bundle的意思我不知道中文怎么解释好，大家意会吧。(**注: 光束法平差**)20世纪下半段，computer vision community开始兴起reconstruction，也开始研究bundle adjustment，一开始重复造轮子，后来triggs**[1]**的modern synthesis及时出现。21世纪前后，robotics领域开始兴起SLAM，最早用的recursive bayesian filter，后来把问题搞成个graph然后用least squares方法解。

---

　　这些东西归根结底就是Gauss大神“发明”的least squares method。当年天文学家Piazzi整天闲得没事看星星，在1801年1月1号早上发现了一个从来没观测到的星星，再接下来的42天里做了19次观测之后这个星星就消失了。当时的天文学家为了确定这玩意到底是什么绞尽了脑汁，这时候Gauss出现了，（最初）只用了3个观察数据，就用least squares算出了这个小行星的轨道，接下来天文学家根据Gauss的预测，也重新发现了这个小行星（虽然有小小的偏差），并将其命名为Ceres，也就是谷神星。Google的ceres-solver就是根据这个来命名的。**ref: ** *How Gauss Determined the Orbit of Ceres.*

　　关于究竟是谁发明了Least Squares历史上有争论，Legendre是最早publish这个方法的（1805），但是几年后（1809）Gauss跳出来说：“你太naive了，我1795年就开始用least squares了，微不足道”。虽然有人认为Gauss这样的大神没必要说谎来和Legendre这种小叼丝（相对，长了一副反派脸）抢成果，但是至今没有definitive的证据证明确实是Gauss最早发明Least Squares。有人认为least squares的方法对Gauss来说太简单以至于Gauss根本没觉得有必要把它publish出来（hehe）。**ref: ** *Gauss and the Invention of Least Squares.*

---

![Gauss](/img/gauss.jpg)
Gauss
![Legendre](/img/legendre.jpg)
Legendre

---

　　我们再来看看19，20世纪连电脑都没有的情况下，geodesy的人们面对的是什么样的问题吧。1927年的North American Datum有25000个观测塔，1983年的NAD有270000个观测塔。再来看看robotics community，最大的real-world SLAM datasets有21,000个pose**[2]**，最大的simulation datasets有200,000个pose**[3]**。看看时间，都是2010年以后的。拿NAD83来说，虽然1983年已经有电脑了，但是优化这样一个network，需要解1,800,000个equations。也就是说如果如果用Least Squares的话，每一步的normal equation J^T * J * x = J^T y 或者Ax = b，里面这个A的dimension是900,000 x 900,000。用dense method光是存这么一个matrix就要3000 Gb**[4]**。

　　Bundle adjustment优化的是sum of reprojection error，这是一个geometric distance（为什么要minimize geometric distance可以参考**[5]**），问题可以formulate成一个least squares problem， 如果nosie是gaussian的话，那就是一个maximum likelihood estimator，是这种情况下所能得到的最优解了。

　　这个reprojection error的公式是非线性的，所以这个least squares problem得用iterative method来求解。最简单的是Newton， 但是要算Hessian，并不是很好算，所以pass。接下来是Gauss-Newton，用J^T J 来近似Hessian，但是convergence速度不给力，也pass。再下来是Levenberg-Marquardt，是一个damping method，改一个lambda来控制到底是偏向steepest descent还是偏向Gauss-Newton，如果算出来更渣的一步就不接受，改个lambda重算，这样一来做了很多无用功，所以也pass。再下来还有Powell's dogleg，是一个trust region method，在这个小区间内搞一个新的function来近objective function，不论好坏都走一步，但是步幅不会超过所谓的trust region，再根据表现调整这个region，总的来说在large scale问题上比Levenberg-Marquardt的表现要好。再往后问题再大就得用前面所说的算法的sparse版本，再大下去得换conjugate gradient方法，这块我就不怎么了解了。

---

　　不论GN,LM,DL，中间都要解一个Ax=b形式的linear system，一般情况下算法的效率就取决于解这个linear system的效率。所以说到底这些nonlinear least squares problem最后也就是解一个linear system。这个linear system你可以直接inverse，也可以用QR，或者Choleskey，或者Schur complement trick来解，爱谁谁。说到这个Choleskey decomposition，当初就是为了Geodetic mapping而发明的。

　　现实中，并不是所有observation都服从i.i.d. gaussian noise的（或者可以说几乎没有），遇到有outlier的情况，这些方法非常容易挂掉，这时候就得用到robust statistics里面的robust cost (*cost也可以叫做loss, 统计学那边喜欢叫risk) function了，比较常用的有huber, cauchy等等。

---

　　总的来说bundle adjustment这个东西搞了这么多年也搞得差不多了，不能说state-of-the-art，但是可以算是gold standard。大点的问题诸如earth-scale reconstruction也被google的人搞过了，用了2 billion张谷歌街景，reconstruct了整个地球，真不知道接下来还能reconstruct什么。

### **Reference**

> 1. **Bundle Adjustment** - A Modern Synthesis, Bill Triggs, et al.
2. H. Johannsson, M. Kaess, M. Fallon, and J. J. Leonard, **“Temporally >scalable visual slam using a reduced pose graph”**, in Proceedings of the IEEE International Conference on Robotics and Automation (ICRA), 2013, pp. 54–61.
3. G. Grisetti, R. Kummerle, C. Stachniss, and W. Burgard, **“A tutorial on graph-based SLAM”**, IEEE Transactions on Intelligent Transportation Systems Magazine, vol. 2, pp. 32–43, 2010.
4. **A Survey of Geodetic Approaches to Mapping and the Relationship to Graph-based SLAM**.
5. **Multiple View Geometry in Computer Vision**, Richard Hartley, Andrew Zisserman.
