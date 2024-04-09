# ParC-Net: Position Aware Circular Convolution with Merits from ConvNets and Transformer



​									2022 ECCV





Transformer很牛，但是在小模型领域convNet在性能和模型复杂度方面仍然具有自己的优势。

为了让Transformer的优点可以应用到小模型，提出了ParC-Net网络，该网络的主干是convnet，同时将Transformer的优点融合到convnet进一步增强convnet在小模型领域的优势。



![image-20230430102301221](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230430102301221.png)















这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 



Transformer和牛，但是在小模型领域convNet在性能和模型复杂度方面仍然具有自己的优势。

为了让Transformer的优点可以应用到小模型，提出了ParC-Net网络，该网络的主干是convnet，同时将Transformer的优点融合到convnet进一步增强convnet在小模型领域的优势。



解决的问题

- 卷积的局部感受野 把卷积的感受野变大
  - 提出位置感知循环卷积（ParC）



这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

**相关研究：**

 自 2017 年以来，随着越来越多的应用程序需要在移动设备上运行 ConvNet 模型，轻量级 ConvNet 备受关注。 现在，有很多轻量级的ConvNets，比如ShuffleNets [24] [24], MobileNets [13] [27] [12], MicroNet [18], GhostNet [10], EfficientNet [32], TinyNet [ 2] 和 MnasNet [31]。 与标准 ConvNets 相比，轻量级 ConvNets 的参数更少





论文中提到的解决方案是什么，关键点在哪儿？

 

1.该结构的vit结构使用了meta-former模块



2.卷积的感受野是局部的，提出位置感知循环卷积ParC增大卷积的感受野







论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）



论文的总结构 上面是以前的常规做法 下面是我们的做法

![image-20230428084729297](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230428084729297.png)



1.使用位置感知循环卷积ParC

![image-20230428090214763](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230428090214763.png)



input + 位置编码  -> 堆叠 -> dw卷积  两个不同位置连接起来 卷积的感受野大大提高

图中*为dw卷积 卷积核的形状为长条    侧面和水平方向做dw卷积



ParC有两种类型

- ParC-V垂直方向 如图a 提取垂直方向感受野
- ParC-H水平方向  如图b 提取水平方向感受野
- 水平 垂直方向插入位置信息

$pe^V$是实例位置嵌入(PE),从基础的$\widetilde{pe}^V$通过双线性插值函数F()生成 ，F()让位置嵌入的大小适应输入特征的大小，EV()函数是垂直方向的展开函数，将输入向量复制w次后，EV() 将这些复制的向量沿水平方向连接起来，生成一个 h×w 大小的 PE 矩阵。

| $\widetilde{pe}^V$ | $pe^V$                       | C X H X W |
| ------------------ | ---------------------------- | --------- |
| 条                 | 面                           | 体        |
| F()双线性插值函数  | EV()函数是垂直方向的展开函数 |           |









用ParC代替self attention



总流程代码

一共四个stages(3:3:9:3)   每个stages包括一个下采样和stage

![image-20230501113013754](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501113013754.png)



stage有两种模块 convNext 和 Parc_Conv

通过判断用哪个模块

![image-20230501113109223](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501113109223.png)



convnext

![image-20230501155923537](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501155923537.png)



parc模块

![image-20230501113442842](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501113442842.png)



parc里的gcc模块

![image-20230501111603322](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501111603322.png)



总的结构为

s = 1 downsample convnext convnext  convnext 

s = 2  downsample  convnext convnext  convnext 

s = 3  downsample  convnext convnext  convnext convnext  convnext  convnext  parc parc parc

s = 4 downsample  convnext convnext parc



用于定量评估的数据集是什么？代码开源的话找到链接（细节）

**实验数据集：**

 







这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

**本文贡献：**

 









下一步还能基于它做什么？有什么工作可以继续深入？（宏观）



