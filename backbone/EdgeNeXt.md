EdgeNeXt: Efficiently Amalgamated CNN-Transformer Architecture for Mobile Vision Applications

用于移动视觉应用的高效合并CNN-Transformer架构

2022 ECCV



现在的网络不断追求准确性，在追求准确性的同时忽略了计算效率，大的网络往往需要很多计算资源 无法部署到边缘设备如机器人，自动驾驶的骑车，因此构建资源高效的通用网络非常重要，所以我们提出了CNN和T的优势 提出一种新的高效混合架构EdgeNeXt。



EdgeNeXt

- split depth-wise transpose attention (STDA) encoder 它将输入张量拆分为多个通道组，并利用深度卷积和跨通道维度的自注意力来隐式增加感受野并编码多尺度特征。

###### ![image-20230423094743794](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423094743794.png)

















这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

现在的网络不断追求准确性，在追求准确性的同时忽略了计算效率，大的网络往往需要很多计算资源 无法部署到边缘设备如机器人，自动驾驶的骑车，因此构建资源高效的通用网络非常重要，所以我们提出了CNN和T的优势 提出一种新的高效混合架构EdgeNeXt。





这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

**相关研究：**

 VIT

MobileVit





论文中提到的解决方案是什么，关键点在哪儿？

CNN局部感受野（快） T全局建模（慢）

CNN结合T利用各自的有点



 提出EdgeNeXt架构

- split depth-wise transpose attention (STDA) encoder 它将输入张量拆分为多个通道组，并利用深度卷积和跨通道维度的自注意力来隐式增加感受野并编码多尺度特征。
- 这个编码器可以学习局部和全局的特征



 高效的自注意力

- cross-covariance attention(交叉协方差注意力)
  - 将自注意力操作合并到特征通道维度而不是相对较少数量的网络块中的空间维度 
  - 复杂度：tokens二次 -> tokens线性 并且有效的隐式编码全局信息
- 我们在我们的 SDTA 编码器 [1] 中使用转置查询和关键注意特征映射。 通过跨通道维度而不是空间维度应用 MSA 的点积运算，此操作具有线性复杂性



自适应内核大小

- 大内核感受野大 但是参数会二次方增长

- 自适应内核大小(网络早期阶段使用较小的内核捕抓低级特征，后期阶段使用较大的内核捕抓高级特征)











论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

![image-20230423094754606](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423094754606.png)



- Conv.Encoder的linear是点卷积 
- DownSampling下采样使用2x2的步长卷积 增加通道数
- SDTA encoder  dw分组卷积直接的箭头是Skip connection



图像分类

ImageNet-1k

- input:256x256
- batchsize 4096
- AdamW
- 300epoch
- learning rate 6e-3
- weight decay 0.05
- cosine learning rate schedule（余炫学习训练计划）

- linear warmup 20epochs

八个a100 30h



![image-20230423111309603](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423111309603.png)





![image-20230423111335630](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423111335630.png)



![image-20230423111355843](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423111355843.png)

语义分割

 ![image-20230423111855002](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423111855002.png)

目标检测

coco

![image-20230423111852354](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423111852354.png)



消融实验

![image-20230423113323273](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423113323273.png)







![image-20230423114302948](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423114302948.png)

![image-20230423114258507](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423114258507.png)

每个阶段使用conv encoder 和 sdta encoder的数量



- 使用Hard-Swish代替GELU
- batch-norm 代替layer-norm



![image-20230423115143826](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423115143826.png)







![image-20230423115253421](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230423115253421.png)



用于定量评估的数据集是什么？代码开源的话找到链接（细节）

**实验数据集：**

 

这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

**本文贡献：**

 

下一步还能基于它做什么？有什么工作可以继续深入？（宏观）