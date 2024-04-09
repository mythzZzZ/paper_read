MetaFormer is Actually What You Need for Vision





最近的研究表明T的注意力模块可以被MLP取代，并且生成的模型效果很好，我们弄了一个PoolFormer并且效果很好





提出MLP模型 PoolFormer

- 使用池化来融合特征











这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 最近的研究表明T的注意力模块可以被MLP取代，并且生成的模型效果很好，我们弄了一个PoolFormer并且效果很好













这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

**相关研究：**

 这篇论文是关于MLP的研究

有关MLP研究的论文  VIP  cycleMLP







论文中提到的解决方案是什么，关键点在哪儿？

 使用MLP结构（PoolingFormer）代替Transformer，让pooling作为 token mixer



![image-20230501093801683](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501093801683.png)



 

论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

metaformer 主要结构



朴实无华只有两个操作

![image-20230501093825302](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501093825302.png)



![image-20230501093947947](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501093947947.png)





ImageNet-1K  分类

![image-20230501094310875](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501094310875.png)



![image-20230501094319862](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230501094319862.png)



分割实验



目标检测



消融实验



1.使用普通的池化层代替token mixer

2.每个块中的池化被替换为全局随机矩阵 使用softmax对每一行进行归一化

3.池化被dw卷积替换



用于定量评估的数据集是什么？代码开源的话找到链接（细节）

**实验数据集：**

ImageNet-1k 分类

Semantic segmentation 分割

 

这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

**本文贡献：**

 

下一步还能基于它做什么？有什么工作可以继续深入？（宏观）