# ROM 以及并行存储器模型

> ROM 的最大特点是1其存储数据的非容易丢失，其访问数据的速度较 `RAM` 来说较低，可以按地址随机访问并在线执行程序，因而在计算机中用于存储固件、引导加载程序、监控程序以及不变或者是很少改变的数据

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330172525.png)



## ROM 的分类

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330172600.png)



### 掩模ROM

即狭义上的 `ROM`，它具有以下的几个特点：

1. 存储内容固定的ROM，由掩模工艺一次性制造

2. 一旦MROM芯片做成，其中的代码与数据将永久保存，且不能够进行修改

3. 用于存储广泛使用的具有标准功能的程序或数据，或用户定做的具有
4. 特殊功能的程序或数据

4. 读取速度比RAM慢很多 



掩模 ROM 结构如下

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330172936.png)



### 可编程 `ROM`

最大的特点就是：用户可以写入内容

可编程ROM分有三种：

1. 一次性编程的PROM 

2. 多次编程的光擦可编程ROM (EPROM)

3. 多次编程的电擦可编程ROM (E2PROM) 



#### 光擦可编程ROM(EPROM)  

下面展示的 `EPROM`  使用浮栅雪崩注入型 `MOS` 管实现存储结构

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330174232.png)

其中 `G1` 被称作是浮空栅，`G2` 被称为是控制栅

当浮空栅上有电子累积时，相当于是存储了 `0`

反之，相当于是存储了 `1`



我们再来看读出时电路

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330174257.png)





1. 行地址译码器的输出 `xi` 和控制栅 `G2` 相连，来决定 `T2` 管是否选中
2. 列地址译码器的输出 `yi` 与 `Ti`  管栅极相连，控制其数据是否读出
3. 当片选信号为高电平时即为选中该片，即读出数据



用光子能量较高的紫外光照射`G1`浮栅时，`G1`中电子获得足够能量，从而穿过氧化层回到衬底中，这样可使浮栅上的`电子消失`，达到抹去存储信息的目的，相当于存储器又存了全`1`



如果要写入 `0`

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330180547.png)





#### 电擦可编程ROM(E2PROM) 

1. 采用电擦除，且擦除速度快

2. 可以按单字节编程和擦除，使用方便

3. 容量比较小，单位成本高

4. 可重复擦除的次数多

5. 用于存储偶尔需要更新的系统配置信息、系统参数、加密保护数据或历史信息等
6. 引脚数量多，封装的尺寸较大，密度较低



#### 闪速(FLASH)存储器   

1. 一种高密度、电擦除、非易失性的只读存储器

2. 既有ROM的优点，又有RAM的优点 

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330180916.png)



##### NOR 闪存

`NOR` 闪存具有以下的特点：

1. 通常称为线性闪存

2. 可以**随机读出任意地址的内容**，读出速度高

3. 存储在其中的**指令可直接执行**

4. 可以对单字节或单字进行编程(编程之前还是需要擦除)

5. 以区块(sector)或芯片为单位执行擦除

6. 有独立的数据线和地址线，接口与`SRAM`相似，信息存储的可靠性高

7. 适合存储监控程序、引导加载程序、系统配置等



##### NAND 闪存

1. 通常称为非线性闪存

2. 每次读出以页(Page)为单位，非随机访问

3. 存储在其中的指令不能够直接执行

4. 以页为单位进行编程

5. 以块(数十页)为单位执行擦除

6. 复用总线，接口与传统ROM不同

7. 不能直接用于存储在线执行的代码，需要增加控制器

8. 适用于大容量存储设备，已部分取代了磁介质存储





## 各种半导体存储器性能的比较

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330181954.png)	



## 并行存储器

> CPU 和主存储之间的速度上的不匹配限制了计算机工作速度
>
> 为了提高 CPU 和主存之间的数据传输率，采用并行技术的存储器



### 双端口存储器

1. 同一个存储器具有两组独立的读写控制线路，是一种高速工作的存储器
2. 两个端口分别具有各自的地址线、数据线和控制线
3. 两个端口可以对存储器中任何位置上的数据进行独立的存取操作



![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330213252.png)



#### 无冲突的读写控制

当两个端口给出的地址不同时，在两个端口上进行读写操作，一定不会发生冲突

当一个端口被选中驱动时，就可以对整个存储器经行存取，每一个端口都有自己的片选控制(CE)，和输出驱动控制(OE)

读操作时，端口的 `OE` 打开驱动器，由存储矩阵读出的数据就出现在 `I/O`线上，其中 `R/WLUB` 和 `R/WLLB` 分别控制高/低字节



下表展示无冲突的读写控制中的各种功能

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330214902.png)



#### 有冲突的读写控制

当两个端口同时存取存储器的一个单元，而且至少有一个端口位写操作时，便发生读写冲突

为了解决这个问题，设定了 `BUSY` 标志位

在这种情况下，**片山的逻辑判断可以决定对哪个端口优先进行读写操作**，而对另一端设置 `BUSY` 标志(`BUSY` 变为低电平)，暂时关闭这个端口

换句话说，写操作对 `BUSY` 变成低电平的端口是不起作用的，只有在优先端口完成操作之后，才能将延迟端口 `BUSY` 标志位恢复，允许延迟端口再进行写操作



总之，当两个端口均为开放状态且存取地址相同时，发生 `写冲突`，此时`仲裁逻辑`可以根据**两个端口的地址匹配或片选信号 `CE` 有效的时间决定对那个端口决心存取**，最后反馈到状态位 `BUSY` 上



判断的方式具体来说就是使用 `CE` 或者是 `地址有效` 两个条件中后发生的来判断

- 如果`地址匹配` 在 `CE` 之前有效，片山更多控制逻辑在 `CEL` 和 `CER` 之间进行判断来选择端口(`CE`判断)
- 如果 `CE` 在 `地址匹配` 之前变低，片上的控制逻辑在左、右地址间进行判断来选择端口(地址有效判断)



具体的判断控制逻辑如下表所示

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/20220330220751.png)



![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/752492543053549135.jpg)





### 多模块交叉存储器

> 与其说多模块交叉存储器是 `并行存储器` 的一种，不如说它是一种设计结构

#### 存储器的模块化组织

一个由若干个模块构成的主存储器是按照线性编址的，这些地址在各模块中有两种编地址方式

- 顺序方式
- 交叉方式

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/169858824593662175.jpg)

可以看出，在顺序存储方式中某个模块进行存取时，其他模块不工作，在一个模块出现故障时，其他的模块可以正常工作，通过扩充模块数量来增加存储容积也比较方便，但是，在取出数据时只能够是串行工作，存储器的带宽受到限制

在交叉方式寻址的过程中，连续地址分布在相邻的不同模块内，对 `连续字成块传送`，可以实现 `多模块流水并行存取`，大大提高存储器的带宽



#### 多模块交叉存储器的结构

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/825037412061620941.jpg)

如图所示，每个存储模块都有自己的读写控制电路、地址寄存器、数据寄存器

`CPU`同时访问四个模块，由存储器控制部件控制它们分别使用数据总线进行信息传递

- 对于一个存储器来说，从 **CPU 给出访存命令直到读出信息仍然使用了一个存取周期的时间**
- 对于 `CPU` 来说，它可以在 **一个存取周期内连续访问四个模块**，各模块的读写过程将 **重叠进行**，所以这种存储器是一种并行存储器结构

下面进行定量分析，假设模块字长与总线宽度相等，假设模块存储器存取一个字的周期为 `T`，总线传输周期为 `t` (CPU 到总线的传输周期)，存储器的交叉模块数为 `m`，为了实现流水线的方式读取，**不让`CPU`“空等”**，如图所示，需要满足：

```shell
T <= mt
# m 的最小值称为 交叉存取度
```

换一种说法，这样设置是为了保证在莫模块启动后经过 `mt` 事件后再访问时，它上次存取操作已经全部完成



贴一道例题：

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/528065857987947733.jpg)



#### 二模块交叉存储器举例

![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/149563468871724910.jpg)

每个模块由 `8` 个 `256k * 4位`的 `DRAM` 芯片构成(位扩展)

地址总线宽度为 `24` 位



从图中可以看出，由 `24位的存储器物理地址`指定的系统主存容量可达 `16MB`，存储地址中按照 `存储体 - 块 - 字` 进行寻址

其中，地址总线的高三位用于存储器选择(字扩展)，一个存储器`2MB`，每个模块有 `8个`

`A20 ~ A3` 18位地址用于模块中`256k`个 `存储字` 的选择，在前面也说过了，它其中的 行/列 9位地址分批送到 `A9 ~ A0`当中

`A2` 是模块选择标志，`A2 == 0` `RAS0` 有效，`A2 == 1` `RAS1` 有效

连续的存储字`32位`交错分布在两个模块上，偶字地址在模块0，奇字地址在模块1



`CPU` 给出字节允许信号 `BE3 ~ BE0`以允许 对`A23 ~ A2`指定的存储字中的字节或字完成读/写访问

当`BE3 ~ BE0`全有效完成字存取，图中没有给出译码逻辑，只暗含了与 `CAS3 ~ CAS0` 的对应关系



`DRAM` 需要定时刷新以防止因为电容漏电而导致的信息丢失，另外，因为 `DRAM` 读是一种 `破坏性读出`，在读出之后要立即按照读出信息予以充电再生

这样，如果 `CPU` 先后两次读取的是同一个模块 (使用同一个 `RAS` 选通信号)，需要在接收到第一个存储字之后进入等待状态直到前一个存储字再生再开始第二个存储字的读取

为此，设计了两个模块，分别由 `RAS0` 和 `RAS1` 进行驱动



![](https://pic22go.oss-cn-beijing.aliyuncs.com/md/249465044799846793.jpg)

上述图是无等待状态下成块存取的示意图，由于采用了 `m = 2`的交叉存取度的成块传送，两个连续地址字之间不必插入等待状态，这称为 `零等待存取`



## 总结

这节主要介绍了 `DRAM` 和我们为提高 `存储器` 与 `CPU` 之间数据传输的速率而设计的两种 `存储器结构技术`



我们从组成各种 `DRAM` 的物理结构开始，定性地分析了各种 `DRAM` 的优劣

接着，我们介绍了使用 `空间并行技术的双端口存储器` 和 `使用时间并行技术实现的多模块交叉存储器`

双端口存储器通过两组独立的互相独立的读写控制电路来实现，为了解决两个模块读写控制上产生的冲突，需要将 `地址有效` 和 `片选有效` 的组合选择的逻辑传送到延迟端口上达到 `独占或者是共享` 的结果

多模块化交叉存储器在不改变硬件结构的基础之上，使用 `流水线` 的思路实现了 `时间维度上的并行操作`，各存储模块之间采用`交叉方式寻址`，大大提高了存储器的带宽

此外，由 `DRAM` 模块实现的多模块交叉存储器，充分利用了读取数据之后的数据再生的时间，使得几个连续地址字之间的读取不必插入等待时间



站在高处看，设计种种存储器结构技术的目的就是为了 **提高速率、向上提供统一的接口、向下屏蔽差异**



<br/><br/>

完

<br/><br/><br/><br/>



---

计算机组成原理小计持续更新，欢迎关注 :smile:
