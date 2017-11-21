# NuclearBomb

首先向各位道歉……本题出现了一些问题。赛后Atum指出，在CUDA函数内的数据同步存在问题，移位操作是在S盒置换操作之后发生的，因此会导致数据不一致，影响解题结果。虽然后续分析后发现这一点可能（至少在出题人机器上）并不会影响最终结果，但还是因此干扰了各位的解题思路。在此就我连续第三年翻车（？）表示诚挚的歉意，希望各位大佬不要穿过网线来线下真人快打。

然后先说一下算法吧，输入的flag是分组处理的，每 `4 byte` 用来初始化一个随机数发生器，之后取出一组随机数用来膨胀成一个数组。之后对数组中的元素按字节进行替换，然后按 `uint32` 进行循环移位（上文中的bug就出现在这里）。结果会和预设的一个数组比较，如果通过，则输入值即为flag。

这一题的坑点有：

1. （再次感谢Atum指出）Nvidia的官方文档对移位指令的描述有问题；
2. 不是所有人都有可以跑CUDA的GPU，一些笔记本的CPU实际是不能跑的；
3. mtrand需要查表爆破，很容易让选手认为思路跑偏。

除了第三点在设计时候是预料到的以外，前两点都是没想到的。第三点当时测试过，跑一轮表最多需要10h（四代移动版i7-4712MQ，16G，单线程，SSD，linux，g++），因此时间上不会出太多问题。但为了避免思路受阻，还是尽量提前放了这道题。

题目源码也在github上开源了，地址为https://github.com/SilverBut/LCTF2017_NuclearBomb 。