# Nand2Tetris

课程目的：带你从0开始构建计算机系统。

前置需求：

- 具备基本的编程能力（任何一门编程语言）。

完成项目所需要的工具：

- [官网](https://www.nand2tetris.org/software)给了Online IDE，其内部集成了.tst和.cmp，类似于OJ。当然，也可以下载这个IDE的Package，并且将.tst和.cmp文件部署到本地
- [nand2teris的论坛](http://nand2tetris-questions-and-answers-forum.52.s1.nabble.com/)

在写笔记前先要声明，本课程的Lecture、课本已经非常全面。为避免我所作的笔记太过抄书化，我就专注于搭建一个框架，从而在我回顾时能高效地get到重点。如有错误、不足之处会陆续优化，还望谅解。

至于具体的Projects，放到了对应的文件夹。

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

​	本章的难点之一在于ALU的设计。当然，本章我们设计的ALU主要是围绕该课程的Hack ALU，如下图所示。

![image-20250324235422561](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250324235422561.png)

至于Hack ALU和我们在实际生产、应用中的ALU之间有什么区别、联系，可以回顾下[视频课的答疑环节](https://www.youtube.com/watch?v=OBCWuMM7ZHc&list=PLrDd_kMiAuNmSb-CKWQqq9oBFN_KNMTaI&index=19)。

## Memory

关于Project3中的第一个Bit.hdl，也指的是Single-Bit Register。下图是关于1-Bit register的黑盒，以及各个时钟周期的变化。![image-20250325165505414](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250325165505414.png)

在Project3-Bit.hdl的设计中，我发现了一个奇怪的东西——DFF。

![image-20250325170304238](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250325170304238.png)

上图也说了**We have to realize a "loading" behavior and a "storing" behavior...**，并且Mux只有选择的作用，那么显然这个DFF在1-Bit register里就是“加载新值”or”存储当前值“的关键部件。

理解了1-Bit register这个东西的大概流程、DFF在其中的作用之后，再来深挖下DFF这个新鲜东西。

DFF（简称D）称作”触发器“，本质是一种时序逻辑原件，在时钟上升沿（或下降沿）捕获输入端的值，并将其保存到输出端，直到下一个时钟边沿到来。DFF的关键特性：

- **同步更新**：输出仅在时钟边沿变化，确保数据更新与时钟同步。
- **状态保持**：在时钟边沿之间，输出保持稳定，不受输入变化的影响。

> [!CAUTION]
>
> 在我的学习过程中，看到了这样1个设计思路：
>
> ```
> Mux(a=out, b=in, sel=load, out=muxOut);
> DFF(in=muxOut, clk=clk, out=out);
> ```
>
> 为啥这个不对呢？
>
> 答：这会导致一种现象，称为”仿真震荡“。
>
> ![image-20250325173455075](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250325173455075.png)
>
> 总而言之，仿真震荡可以理解为**组合逻辑环路导致信号值无限递归计算**。
>
> 那如何设计才能避免呢？
>
> ![image-20250325173638917](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250325173638917.png)
>
> 而在实际的芯片设计中，有个设计准则——**任何反馈路径必须经过时序元件（如 DFF），否则必然导致仿真震荡或电路不稳定**。
>
> ![image-20250325173649219](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250325173649219.png)

Project3-Register.hdl的设计可以完全基于Bit.hdl，如下图所示。

![image-20250325174900899](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250325174900899.png)

而RAMn.hdl的设计也可以完全基于Register.hdl，如下图所示。

![image-20250325175059392](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250325175059392.png)

如果只是停留在Abstraction这一阶段，那看起来非常简单，像是从上到下叠在一起。但如果想要真正地Implementation，各个register到底该如何组合到一起是一门学问。

![image-20250326213002761](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250326213002761.png)



接下来是PC。lecture里画的太简洁了根本无从下手，于是我找了下面这张图。

![HDL API & Gate Design](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\pc.png)

> [!IMPORTANT]
>
> 但为啥优先级要设置为inc>load>reset呢？如果按照下图这样的分支结构，难道第一优先级不应该是reset吗？
>
> ![image-20250326222205075](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250326222205075.png)
>
> 我在[stackoverflow](https://stackoverflow.com/questions/15034037/trying-to-build-a-pc-counter-for-the-nand2tetris-book-but-im-having-some-tro)上也看见了类似的问题。
>
> 答：没有错，第一优先级确实是reset。但在设计上，它就应该在最后一个。举个极端的例子，若reset==0，则经过前面的inc、load后取的值无论是什么，经过reset后的取值都是0。
>
> 事实上，在多路选择器链中，最后一个Mux的选择器具有最高优先级，因为它位于链的末端，极端情况下甚至可以覆盖前面的所有选择。
>
> ![image-20250326221807868](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250326221807868.png)

最后是RAMn。同理，lecture中的描述太过简单。

![image-20250327000809507](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250327000809507.png)

![img](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\ram8.png)



至此RAMn的设计基本完结。

在设计RAMn这一Project中，我在论坛翻到了[一个被admin说成是way off the mark的设计方案](http://nand2tetris-questions-and-answers-forum.52.s1.nabble.com/ABOUT-RAM-td4036525.html)，感觉蛮有趣。



## Machine Language



**The syntax of Machine Languages varies across computers.**

![image-20250325160232864](D:\Study\Computer_Science\Architecture\Nand2Tetris\Notebook\images\image-20250325160232864.png)

