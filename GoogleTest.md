#  GoogleTest

googletest是一个google的一个c++测试框架

## Assertions

googtest's assertions是类似于函数调用的宏，我们可以通过assert行为来测试类或函数。 assert失败时，googletest会输出assert的源文件和行号位置以及失败消息。 我们还可以提供自定义失败消息，该消息将附加到googletest的消息.

assert成对出现，测试相同的事物，但是对当前函数有不同的影响

**ASSERT_***：生成致命错误，并且终止当前函数

**EXPECT_***：生成非致命错误，并且不终止当前函数

通常使用**EXPECT_*** 更好，它允许报告多个错误，如果当前程序发生错误而继续运行没有意义应该使用 **ASSERT_***

要提供自定义的失败消息，只需使用<<操作符或此类操作符序列将其流到宏中

```c++
ASSERT_EQ(x.size(), y.size()) << "Vectors x and y are of unequal length";

for (int i = 0; i < x.size(); ++i) {
  EXPECT_EQ(x[i], y[i]) << "Vectors x and y differ at index " << i;
}
```

## Basic Assertions

![image-20201127174644094](C:\Users\ytn\AppData\Roaming\Typora\typora-user-images\image-20201127174644094.png)

## Binary Comparison

比较两个值

![image-20201127174809598](C:\Users\ytn\AppData\Roaming\Typora\typora-user-images\image-20201127174809598.png)

值参数必须是可由assert的比较运算符进行比较，否则会出现就会出现错误。当然这些assertions也可以使用我们自定义的类型，但是前提是我们必须定义了相应的比较运算符。但google c++ style并不推荐这样做。

ASSERT_EQ()判断相等时是对指针进行比较，因此如果在两个c风格字符串上使用，它将测试他们是否在相同的内存位置，而不是他们的值是否相同。如果要比较两个值是否相等，则可以使用ASSERT_STREQ()，要比较两个字符串对象则使用ASSERT_EQ()，比较空指针则请使用*_EQ(ptr,nullptr)。

## String Comparison

此assertions是用来比较c字符串。

![image-20201127195547162](C:\Users\ytn\AppData\Roaming\Typora\typora-user-images\image-20201127195547162.png)

assert名称中的“ CASE”表示忽略大小写。 NULL指针和空字符串被认为是不同的。

## Simple Tests

创建一个test:

* 使用TEST()宏去定义和命名一个测试函数，这些事没有返回值的普通c++函数
* 在此函数中，使用各种googletest的assertions去检查值
* 测试的结果由assertions断定

```c++
TEST(TestSuiteName, TestName) {
  ... test body ...
}
```

TEST（）参数从通用到特定。 第一个参数是测试套件的名称，第二个参数是测试套件内的测试名称。 这两个名称都必须是有效的C ++标识符，并且它们不应包含任何下划线（_）。 测试的全名包括其包含的测试套件及其个人名称。 来自不同测试套件的测试可以具有相同的个人名称。

例如有如下函数

```c++
int Factorial(int n);  // Returns the factorial of n
```

所得的测试套件如下：

```c++
// Tests factorial of 0.
TEST(FactorialTest, HandlesZeroInput) {
  EXPECT_EQ(Factorial(0), 1);
}

// Tests factorial of positive numbers.
TEST(FactorialTest, HandlesPositiveInput) {
  EXPECT_EQ(Factorial(1), 1);
  EXPECT_EQ(Factorial(2), 2);
  EXPECT_EQ(Factorial(3), 6);
  EXPECT_EQ(Factorial(8), 40320);
}
```

## 测试装置fixture：对多个测试使用相同的数据配置

步骤：

* 从::testing::Test派生一个类，并且为protected
* 在类的内部，声明计划去使用的任何对象
* 如有必要，编写默认构造函数或SetUp()函数为每个测试准备对象
* 如有必要，编写析构函数或TearDown()函数在构造函数中申请的资源
* 如有必要，定义要共享的测试子例程

当使用一个装置是，使用**TEST_F()**代替**TEST()**

```c++
TEST_F(TestFixtureName, TestName) {
  ... test body ...
}
```

第一个参数是测试套件名称，但是对于TEST_F（），它必须是fixture类的名称

C ++宏系统不允许我们创建可以处理两种类型的测试的单个宏。 使用错误的宏会导致编译器错误。