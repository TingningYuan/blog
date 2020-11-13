# 2-OpenBLAS简介

## 什么是BLAS

![image-20201113101135208](C:\Users\ytn\AppData\Roaming\Typora\typora-user-images\image-20201113101135208.png)

## 如何在C中调用

如果我们想在自己的C语言代码中调用BLAS的函数，可以去http://netlib.org/blas/index.html#_blas_routines网站查看CBLAS提供的C语言接口。另外在链接的时候需要加上**-lopenblas**,下面是一个调用的例子：

```c
#include <cblas.h>
...
cblas_sgemm(CblasRowMajor, CblasNoTrans, CblasNoTrans, M, N, K, 1.0, A, K, B, N, 0.0, result, N);
```

![img](https://petewarden.files.wordpress.com/2015/04/gemm_corrected.png)

## OpenBLAS vs GotoBLAS

	*	优化了L3在Intel Sandy Bridge 64-bit OS
	*	优化了L3在ICT Loongson-3A
	*	修复了一些BUGS
	*	增加了一些次要的元素



## OpenBLAS的一些实现

### 内存分配

在OpenBLAS中，通过管理一个内存池来进行内存分配，可分配的数量通过如下来定义：

```c
#define NUM_BUFFERS (MAX_CPU_NUMBER * 2)
```

