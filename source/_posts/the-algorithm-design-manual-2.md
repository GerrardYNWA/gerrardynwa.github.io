title: 《The Algorithm Design Manual》第二章
date: 2019-03-16 15:55:17
categories: Algorithm
tags: [interview problems]
---

《The ALgorithm Design Manual(2nd Ed.)》俗称算法中的红宝书，其第一部分讨论实用算法思路，第二部分进行实例分析，这本ADM相比CLRS显得通俗易懂许多，而且侧重在算法设计的思路上，很适合进行闲时翻阅和面试备战。
　　以下将分几个小节讲述第二章的内容要点和课后习题，课后习题主要讲解其中的Interview Problems。

<!--more-->

### Chapter 2. Algorithm Analysis

#### 内容要点

#### 课后习题
###### Interview Problems
+ 2-43. You are given a set $S$ of $n$ numbers. You must pick a subset $S'$ of $k$ numbers from $S$ such that the probablity of each elements of $S$ occurring in $S'$ is equal (i.e., each is selected with probability $k/n$). You may make only one pass over the numbers. What if $n$ is unknown?

+ 2-44. We have 1,000 data items to store on 1,000 nodes. Each node can store copies of exactly three different items. Propose a replication scheme to minimize data loss as nodes fail. What is the expected number of data entries that get lost when three random nodes fail?
 
+ 2-45. Consider the following algorithm to find the minimum element in an array of numbers $A[0，...，n]$. One extra variable tmp is allocated to hold the current minimum value. Start from *A[0]*; *”tmp”* is compared against $A[1]，A[2]，...，A[N]$ in order. When $A[i] < tmp$, $tmp = A[i]$. What is the expected number of times that the assignment operation $tmp = A[i]$ is performed?

+ 2-46. You have a 100-story building and a couple of marbles. You must dentify the lowest floor for which a marble will break if you drop it from this floor. How fast can you find this floor if you are given an infinite supply of marbles? What if you have only two marbles?

+ 2-47. You are given 10 bags of gold coins. Nine bags contain coins that each weigh 10 grams. One bag contains all false coins that weigh one gram less. You must identify this bag in just one weighing. You have a digital balance that reports the weight of what is placed on it.

+ 2-48. You have eight balls all of the same size. Seven of them weigh the same, and one of them weighs slightly more. How can you find the ball that is heavier by using a balance and only two weighings?

+ 2-49. Suppose we start with $n$ companies that eventually merge into one big company. How many different ways are there for them to merge?

+ 2-50. A **Ramanujam number** can be written two different ways as the sum of two cubes—i.e., there exist distinct $a, b, c$, and $d$ such that $a^3 + b^3 = c^3 + d^3$. Generate all Ramanujam numbers where $a, b, c, d < n$.

+ 2-51. Six pirates must divide $300 dollars among themselves. The division is to proceed as follows. The senior pirate proposes a way to divide the money. Then the pirates vote. If the senior pirate gets at least half the votes he wins, and that division remains. If he doesn’t, he is killed and then the next senior-most pirate gets a chance to do the division. Now you have to tell what will happen and why (i.e., how many pirates survive and how the division is done)? All the pirates are intelligent and the first priority is to stay alive and the next priority is to get as much money as possible.

+ 2-52. Reconsider the pirate problem above, where only one indivisible dollar is to be divided. Who gets the dollar and how many are killed?



 
