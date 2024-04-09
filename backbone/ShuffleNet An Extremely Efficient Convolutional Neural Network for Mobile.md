# ShuffleNet: An Extremely Efficient Convolutional Neural Network for Mobile







这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 

介绍了一种计算效率极高的CNN架构ShuffleNet









论文中提到的解决方案是什么，关键点在哪儿？



 1x1Gconv  扩展不同组的特征图的通道

![image-20230713200735759](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230713200735759.png)

 



shuffleNet的结构

![image-20230713201100132](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230713201100132.png)



shuffle操作就是打乱特征图通道的拼接顺序，让不同组的特征图通道拼在一起









