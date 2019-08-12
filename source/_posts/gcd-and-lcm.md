title: GCD和LCM
date: 2019-01-12 15:44:58
categories: Algorithm

tags: [interview problems]
---

　　整数a、b的最大公约数(Greatest Common Divider, GCD)和最小公倍数(Least Common Multiple, LCM)的证明及求法

<!-- more -->

## 1. 最大公约数(Greatest Common Divider, GCD)

　　所谓求整数$a$、$b$的最大公约数，就是求同时满足$a \% c = 0$、$b \% c = 0$的最大正整数$c$，即求能够同时整除$a$和$b$的最大正整数$c$。

### 1.1 欧几里得算法（辗转相除法）

　　若$a$、$b$全为0，则它们的最大公约数不存在；若$a$、$b$其中之一为0，则它们的最大公约数为非0的那个；若$a$、$b$都不为0，则使新$a = b$; 新$b = a\%b$，然后重复该过程。

### 1.2 证明

#### A. 证明$a$和$b$的公约数同时也是$b$和($a$ mod $b$)的公约数

> 若整数$g$为$a$和$b$的公约数(不同时为0)，则$g$满足：
> 
> $$
> a = g * p \\
> b = g * q \tag{1}
> $$
> 
> 其中$p$、$q$为整数，同时$a$又可以由$b$表示为：
> 
> $$
> a = k * b + t \tag{2}
> $$
> 其中$k=a/b$为整数，$t=a%b$，则将(1)式代入(2)中，替换掉$a$和$b$：
> 
> $$
> \begin{equation}
> \begin{aligned}
> g * p &= k * g * q + t \\
>    t &= g * (p - k * q)
> \end{aligned}
> \end{equation} \tag{3}
> $$
> 由上式可知$a$和$b$的公约数同是$b$和($a$ mod $b$)的公约数。

#### B. 证明若$g$是$a$和$b$的最大公约数，它同样也是$b$和($a$ mod $b$)的最大公约数

> 假设$g$时$a$和$b$的最大公约数，但不是$b$和($a$ mod $b$)的最大公约数，即存在$$g^{'}>g$$且$$g^{'}$$同时整除$b$和($a$ mod $b$)。则必存在整数$p$和$q$使得下式成立：
> $$
> \begin{equation}
> \begin{aligned}
> b &= g^{'}*p^{'} \\
> a \% b = t &= g^{'}*q^{'}
> \end{aligned}
> \end{equation} \tag{4}
> $$
> 同时，$a$、$b$、$t$之间满足：
> $$
> a = k * b + t \tag{5}
> $$
> 将(4)式代入(5)式中得：
> $$
> \begin{equation}
> \begin{aligned}
> a &= k * g^{'} * p^{'} + g^{'} * q^{'} \\
> &= g^{'} * (k * p^{'} + q^{'})
> \end{aligned}
> \end{equation} \tag{6}
> $$
>
> 即$$g^{'}$$也同时整除$a$，即也是$a$和$b$的公约数，与假设矛盾，即得证。

　　这样，我们把求$a$、$b$的最大公约数转化成了求$b$和($a$ mod $b$)的最大公约数，那么问题不变而数据规模明显变小。我们可以不断重复该过程，直到问题缩小成某个非零数与零的最大公约数。这样，所求的非零数即为最大公约数。

### 1.3 代码

```C++
/*
解法一：递归
*/
int GCD(int a, int b) { // a和b不同时为0
  if (b == 0) return a;
  
  return GCD(b, a % b);
}

/*
解法二：迭代
*/
int GCD(int a, int b) { // a和b不同时为0
  while (b) {
    a = a % b;
    swap(a, b);
  }
  
  return a;
}
```

## 2. 最小公倍数(Least Common Multiple, LCM)

　　求整数a和b的最小公倍数，即求最小正整数$c$，使得$c\%a=0$且$c\%b=0$。

### 2.1 结论

　　$a$和$b$两数的最小公倍数为两数的乘积除以它们的最大公约数。

### 2.2 证明

> 首先明确$k = a * b$一定是$a$和$b$的一个公倍数，那么最小公倍数一定不大于$k$，那么对于$a$和$b$的最大公约数$c$，则有：
> $$
> \begin{equation}
> \begin{aligned}
>     k &= a * b       \\
> k / c &= a * b / c   \\
> k / c &= a * (b / c) \\
> k / c &= b * (a / c)
> \end{aligned}
> \end{equation} \tag{7}
> $$
> 其中$b/c$和$a/c$均为整数，即$k/c$同时是$a$和$b$的倍数；反之，若$c$不为$a$和$b$的公约数，则$b/c$和$a/c$至少有一个不是整数，则$k/c$不是$a$和$b$的公倍数。显然，我们要取得最小的公倍数，即找到最大的公约数$c$使得$k/c$最小，该$k/c$就是我们要求的最小公倍数。