# Run, Don’t Walk: Chasing Higher FLOPS for Faster Neural Networks



FLOPS：每秒浮点运算次数，用来形容显卡的性能

FLOPs：用来形容模型的复杂度





这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 使用dw卷积时，==FLOPS的效率低下==并证明如此低的 FLOPS 主要是由于算子的频繁内存访问





 

论文中提到的解决方案是什么，关键点在哪儿？

 我们提出了一种新颖的部分卷积（==PConv==），通过同时减少冗余计算和内存访问，更有效地提取空间特征。



什么是PConv

只卷一部分通道，其他通道不卷

![image-20230701111219811](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230701111219811.png)





PConv后使用 1x1的pwconv构成一个T形结构

![image-20230701164747107](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230701164747107.png)



它们在输入特征图上的有效感受野看起来像一个 T 形 Conv，与统一处理补丁的常规 Conv 相比，它更关注中心位置（salient position ）。

通过Frobenius 范数计算公式计算得知，中心位置的权重大于周围邻居的计算权重，然后作者通过实验证明了这一点。由此说明使用T形卷积的运用对特征图非常有效

![image-20230701165358724](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230701165358724.png)







 





论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

首先检查 PConv 的计算速度及其与 PWConv 结合使用时的有效性。然后，我们全面评估 FasterNet 在分类、检测和分割任务方面的性能。 最后，我们进行了简短的消融研究。