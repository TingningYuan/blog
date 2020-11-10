# OpenBLAS:(1)ubuntu18.04安装与测试

今天开始学习OpenBLAS，所以专门开设一个系列来记录一下。登录OpenBLAS可以看到该项目的详细信息：[GitHub - xianyi/OpenBLAS: OpenBLAS is an optimized BLAS library based on GotoBLAS2 1.13 BSD version.](https://github.com/xianyi/OpenBLAS)

## 1：安装OpenBLAS

```c
git clone https://github.com/xianyi/OpenBLAS.git

cd OpenBLAS

make

sudo make install PREFIX=/usr/local/OpenBLAS  //将其安装在/usr/locl/OpenBLAS下
```

上面再安装时完全遵照上面即可，不需要自己新建一个build文件夹（多此一举踩坑泪）

## 2：测试是否安装成功

```c
vim test.c
```

```c
  1 #include<cblas.h>
  2 #include<stdio.h>
  3 
  4 int main()
  5 {
  6     int i=0;
  7     double A[6]={1.0,2.0,1.0,-3.0,4.0,-1.0};
  8     double B[6]={1.0,2.0,1.0,-3.0,4.0,-1.0};
  9     double C[9]={.5,.5,.5,.5,.5,.5,.5,.5,.5};
 10     cblas_dgemm(CblasColMajor,CblasNoTrans,CblasTrans,3,3,2,1,A,
 11                 3,B,3,2,C,3);
 12 
 13     for(i=0;i<9;i++){
 14         printf("%f ",C[i]);                                                           
 15     }
 16     printf("\n");
 17     return 0;
 18 }
```

使用如下命令运行

```c
gcc -o test test.c /usr/local/lib/libopenblas.a 
```

如果出现下面结果则说明安装成功

![image-20201110165916903](C:\Users\ytn\AppData\Roaming\Typora\typora-user-images\image-20201110165916903.png)

