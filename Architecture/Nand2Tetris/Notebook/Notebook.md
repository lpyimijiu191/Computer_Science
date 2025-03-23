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

#### Actual Hardware Construction

#### HDL（Hardware Description Language）

#### Hardware Simulation

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

本章最难的点就是Multi-way variants。由于Or8Way太简单，那就举一个Mux4Way16的例子吧。当然，它可以用我们之间已经设计出的Mux16来实现。

![img](.\images\mux4.png)

至于之后的各种DMux，如果自己想不出来，可以参考[这个网站](https://nand2tetris-hdl.github.io/)。

在本章的最后，要学会使用Hack chip set API。例如，当我们不知道HDL语言中的输入、输出引脚名称时，可以随时查阅。

![image-20250321232625265](.\images\image-20250321232625265.png)

## Boolean Arithmetic

![image-20250323163627566](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250323163627566.png)

上图是众所周知的冯诺依曼计算机体系结构。由于在本章主要讨论Arithmetic，因此十分有必要将CPU中的ALU单独拿出来讨论。

![image-20250323163828945](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250323163828945.png)

经过思考，为了让ALU能顺利、简单地实现Arithmetic操作，我们对+、-、*、/这4种基本的Arithmetic操作的实现方法如下图所示。

![image-20250323164351099](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250323164351099.png)

![image-20250323164531424](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250323164531424.png)

现在从逻辑上我们思考出了一种比较合理的Addition算法，并且也有相应的办法处理了所谓的Overflow（即便是无视它）。之后就是设计出一种名为Adder的硬件，来作为实现这种Addition算法的载体。

![image-20250323164654720](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250323164654720.png)

关于这个FullAdder，可以用2个HalfAdder实现。如下图所示。

![image](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\9300b3b0dfbd45418c3f9b5e6d975804.png)



