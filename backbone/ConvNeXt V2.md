# ConvNeXt V2: Co-designing and Scaling ConvNets with Masked Autoencoders

使用 Masked Autoencoders 共同设计和缩放 ConvNet



在ConvNeXt中添加自监督学习技术

- 提出了一个完全卷积掩码自动编码器框架（fully convolutional masked autoencoder framework）(FCMAE)

  - 使用全卷积掩码自动编码器框架进行了**预训练**

- 一个新的全局响应归一化 (GRN) 层，可以将其添加到 ConvNeXt 架构中以增强通道间特征竞争。

  





Fully Convolutional Masked Autoencoder (FCMAE)

- 传统的MAE基于Vit提出来把patch加噪声弄模糊 在用来预训练
- 若想在卷积上用MAE传统的用在vit上的方法不行因为它遮住的是patch
  - 转换过来卷积上应当是遮住卷积操作时的部分元素
  - 所以提出了fc mae
    - 输入input 遮住  然后输入encode
    - ![image-20230418110251107](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230418110251107.png)



encode

- 改装ConvNeXt架构
  - 把ConvNeXt里的conv改成稀疏卷积（submanifold sparse convolution）处理可见部分





ConvNeXt架构和FCMAE预训练架构共同设计用于使基于掩码的自监督预训练取得成功





GRN层（解决**Feature collapse** 现象）

- 全局响应归一化 （FCMAE进行特征映射的时候会发现一些特征映射饱和，激活在通道之间变得多余）
- GRN包括三个步骤
  - 全局特征聚合
  - 特征归一化
  - 特征校准









## 这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 前有ConvNeXt模仿Transformer结构得到很好的效果，这次Transformer出现了mask的训练方法，

用conv实现Transformer的mask方法







## 论文中提到的解决方案是什么，关键点在哪儿？

 1.要实现mask的训练方法，需要自监督训练技术 MAE

- 本文提出完全卷积掩码自动编码器框架（卷积版的MAE）

- 新的全局响应归一化层(GRN) 

  



 

卷积版的MAE实现

- 使用稀疏卷积来mask掉特征的一部分





当使用卷积版的MAE时，作者发现MLP层潜在特征崩溃，此时加入GRN层解决这个问题

GRN层的作用

- 把这些架构添加到ConvNeXt架构中可以增强通道间特征竞争



==Fully Convolutional Masked Autoencoder==

方法在概念上很简单，并且以完全卷积的方式运行。 学习信号是通过以高屏蔽率随机屏蔽原始输入视觉效果并让模型在给定剩余上下文的情况下预测缺失部分来生成的

- 使用基于稀疏卷积的ConvNeXt实现FCMA
- 自动编码器的架构是不对称的。 编码器仅处理可见像素，解码器使用编码像素和掩码标记重建图像。 损失仅在屏蔽区域上计算。
- 掩蔽比为 0.6 的随机掩蔽策略
- 重建目标 计算重建图像和目标图像之间的均方误差 MSE



==GRN层对神经元进行侧向抑制==

1.为什么需要进行侧抑制？

作者通过计算特征图通道间的距离得出，ConvNeXt MAE网络存在特征崩溃现象，此时对神经元进行侧向抑制可以促进神经元的多样性。（大脑中有许多促进神经元多样性的机制。 例如，侧向抑制 [6, 30] 可以帮助增强激活神经元的反应，增加单个神经元对刺激的对比度和选择性，同时还可以增加整个神经元群的反应多样性）

深度学习中这种侧向抑制通过GRN层来实现

所提出的 GRN 单元包括三个步骤：1) 全局特征聚合，2) 特征归一化，以及 3) 特征校准。



GRN

![image-20230621115628197](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230621115628197.png)

Gx：计算标准差

Nx：利用标准差进行归一化

![image-20230621115725977](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230621115725977.png)









## 论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

本文使用了FCMAE 预训练框架和 ConvNeXt V2 架构，它们共同设计用于使基于掩码的自监督预训练取得成功 









用于定量评估的数据集是什么？代码开源的话找到链接（细节）

实验数据集：

 

这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

本文贡献：

 

下一步还能基于它做什么？有什么工作可以继续深入？（宏观）













































数据集

- COCO
- ADE20K
- ImageNet







这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 

这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

**相关研究：**

 

论文中提到的解决方案是什么，关键点在哪儿？

 

 

论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

用于定量评估的数据集是什么？代码开源的话找到链接（细节）

**实验数据集：**

 

这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

**本文贡献：**

 

下一步还能基于它做什么？有什么工作可以继续深入？（宏观）




$$

$$
