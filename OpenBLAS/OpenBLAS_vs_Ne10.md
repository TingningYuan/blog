# OpenBLAS vs Ne10

## 1-官网地址

OpenBLAS:https://www.openblas.net/

Ne10:https://projectne10.github.io/Ne10/

## 2-项目简介

### OpenBLAS

OpenBLAS是基于GotoBLAS2 1.13 BSD版本的优化的基本线性代数子程序（BLAS）库。

维基百科： https://github.com/xianyi/OpenBLAS/wiki.

### Ne10

Ne10是开源的库，它已针对配备NEON SIMD功能的基于Arm的CPU进行了优化。可以通过静态或动态链接轻松地集成到各种应用程序中。该库提供了一些适用于Arm v7-A和v8-A架构关键操作的开源实现，尤其着重于数学、信号处理、图像处理和物理功能

维基百科：https://wiki.cdot.senecacollege.ca/wiki/Ne10_library

## 3-遵循的开源协议

OpenBLAS:BSD

Ne10:BSD

## 4-代码仓库

OpenBLAS:https://github.com/xianyi/OpenBLAS

Ne10:https://github.com/projectNe10/Ne10

## 5-开发语言

**OpenBLAS**:C/Fortan

**Ne10**:C

## 6-包含模块

### OpenBLAS

Level1：标量、向量、向量与向量操作            
Level2：矩阵与向量操作
Level3：矩阵与矩阵操作     

### Ne10

math 数学模块：主要包含矢量/矩阵数学运算 

dsp 数字信号处理模块：主要包含FFT快速傅立叶变换，以及部分FIR/IIR滤波函数

imgproc 图像处理模块：主要包含图像缩放，旋转等图像后处理函数

physics 物理模块：主要包含物理方面的一些处理函数

## 7-遵循的API规范

**OpenBLAS**:

**Ne10**:遵循Linux kernel中的C语言编码格式：[Linux kernel](https://www.kernel.org/doc/Documentation/CodingStyle)



## 8-工具编译链接配置

### OpenBLAS

https://github.com/xianyi/OpenBLAS/wiki/User-Manual

#### 正常编译

make/gmake(BSD)，若要设置特定的目标CPU,可以使用TARGET=xxx

#### 交叉编译

Set `CC` and `FC` to point to the cross toolchains, and set `HOSTCC` to your host C compiler. The target must be specified explicitly when cross compiling.

Examples:

- On an x86 box, compile this library for a loongson3a CPU:

  ```makefile
  make BINARY=64 CC=mips64el-unknown-linux-gnu-gcc FC=mips64el-unknown-linux-gnu-gfortran HOSTCC=gcc TARGET=LOONGSON3A
  ```

  or same with the newer mips-crosscompiler put out by Loongson that defaults to the 32bit ABI:

  ```makefile
  make HOSTCC=gcc CC='/opt/mips-loongson-gcc7.3-linux-gnu/2019.06-29/bin/mips-linux-gnu-gcc -mabi=64' FC='/opt/mips-loongson-gcc7.3-linux-gnu/2019.06-29/bin/mips-linux-gnu-gfortran -mabi=64' TARGET=LOONGSON3A
  ```

- On an x86 box, compile this library for a loongson3a CPU with loongcc (based on Open64) compiler:

  ```makefile
  make CC=loongcc FC=loongf95 HOSTCC=gcc TARGET=LOONGSON3A CROSS=1 CROSS_SUFFIX=mips64el-st-linux-gnu-   NO_LAPACKE=1 NO_SHARED=1 BINARY=32
  ```

**静态链接**：libopenblas.a

**动态链接**：-lopenblas

### Ne10

详见链接：https://github.com/projectNe10/Ne10/blob/master/doc/building.md#building-ne10

## 9-是否有完整的测试套件

是

## 10-应用案例



