title: CUDA——从入门到转行(一)
date: 2016-08-09 08:28:24
categories: Column
tags: [cuda]
---

　　CUDA，Compute Unified Device Architecture的简称，是由NVIDIA公司创立的基于他们公司生产的图形处理器GPUs（Graphics Processing Units,可以通俗的理解为显卡）的一个并行计算平台和编程模型。

　　通过CUDA，GPUs可以很方便地被用来进行通用计算（有点像在CPU中进行的数值计算等等）。在没有CUDA之前，GPUs一般只用来进行图形渲染（如通过OpenGL，DirectX）。

　　开发人员可以通过调用CUDA的API来进行并行编程，达到高性能计算目的。NVIDIA公司为了吸引更多的开发人员，对CUDA进行了编程语言扩展，如CUDA C/C++、CUDA Fortran语言。注意CUDA C/C++可以看作一个新的编程语言，因为NVIDIA配置了相应的编译器nvcc。

<!-- more -->

　　GPU并不是一个独立运行的计算平台，而需要与CPU协同工作，可以看成是CPU的协处理器，因此当我们在说GPU并行计算时，其实是指的基于CPU+GPU的异构计算架构。在异构计算架构中，GPU与CPU通过PCIe总线连接在一起来协同工作，CPU所在位置称为为主机端（host），而GPU所在位置称为设备端（device）。

<center>![基于CPU+GPU的异构计算](/img/cuda1-1.jpg)</center>

　　可以看到GPU包括更多的运算核心，其特别适合数据并行的计算密集型任务，如大型矩阵运算，而CPU的运算核心较少，但是其可以实现复杂的逻辑运算，因此其适合控制密集型任务。另外，CPU上的线程是重量级的，上下文切换开销大，但是GPU由于存在很多核心，其线程是轻量级的。因此，基于CPU+GPU的异构计算平台可以优势互补，CPU负责处理逻辑复杂的串行程序，而GPU重点处理数据密集型的并行计算程序，从而发挥最大功效。

<center>![基于CPU+GPU的异构计算应用执行逻辑](/img/cuda1-2.jpg)</center>