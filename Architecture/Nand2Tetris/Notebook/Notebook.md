# Nand2Tetris

课程目的：带你从0开始构建计算机系统。

前置需求：具备基本的编程能力（任何一门编程语言）。

完成项目所需要的工具：[官网](https://www.nand2tetris.org/software)给了Online IDE，其内部集成了.tst和.cmp，类似于OJ。当然，也可以下载这个IDE的Package，并且将.tst和.cmp文件部署到本地。

在写笔记前先要声明，本课程的Lecture、课本已经非常全面。为避免我所作的笔记太过抄书化，我就专注于搭建一个框架，从而在我回顾时能高效地get到重点。至于具体的Projects，我单独放到了对应的文件夹。

## Boolean Logic

本章用原始的逻辑门“与非门”，来构建其它逻辑门——Any Boolean function can be realized using **only Nand**.

### Background

#### Boolean Algebra

Boolean function——A function that operates on **boolean variables**, and returns **a boolean value**.

描述布尔函数的方法，

- Truth Table Representation

- Boolean Expressions

- Canonical Representation

- Two-Input Boolean Functions

    这个乍一看比较晦涩。其实就是给定你$n$个变量的Boolean Function，而每个变量的值可以是0/1，那么显然输入有$2^n$种情况。并且Boolean Function必须要输出一个函数值，这个函数值的每一位都是0/1，因此对应共$2^{2^n}$种函数。

#### Gate Logic

由于在这里的关注重点是logic，因此类似于电路一样physical的东西（如下图所示），暂不关注。

![image-20250321131734452](.\images\image-20250321131734452.png)

此外，在本书中，Nand门被认为是原始的逻辑结构，所以没有必要去构建它：只要你在HDL程序中使用Nand门，仿真器就会自动地调用其内置的tools/builtIn/Nand.hdl工 具。

![image-20250321150447067](.\images\image-20250321150447067.png)

![image-20250321131917321](.\images\image-20250321131917321.png)

And3（乃至Andn），可以用2个And门来实现。

![image-20250321132001010](.\images\image-20250321132001010.png)

![image-20250321132015367](.\images\image-20250321132015367.png)

首先遇到需要思考的是Xor。

![image-20250321132046977](.\images\image-20250321132046977.png)

![image-20250321132226731](.\images\image-20250321132226731.png)

![image-20250321132346519](.\images\image-20250321132346519.png)MUX这个东西见到的不是很多，看了[这篇博客](https://blog.csdn.net/vivid117/article/details/100747939)就找到了MUX（这里只讨论**2路选择MUX**)，如下图所示。

![image-20250321140321091](.\images\image-20250321140321091.png)

DMUX也是同理。

![image-20250321141914505](.\images\image-20250321141914505.png)

![image-20250321231353381](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250321231353381.png)

为了进一步理解DMUX，可以看下[这个视频](https://www.youtube.com/watch?v=O6YdxnYcTvM)。

至于MUX、DMUX的作用，可以看下图。

![image-20250321231835228](.\images\image-20250321231835228.png)

在本章的最后，要学会使用Hack chip set API。例如，当我们不知道HDL语言中的输入、输出引脚名称时，可以随时查阅。

![image-20250321232625265](.\images\image-20250321232625265.png)

#### Actual Hardware Construction

#### HDL（Hardware Description Language）

#### Hardware Simulation

### Specification



