DMFORMER CLOSING THE GAP BETWEEN CNN AND VISION TRANSFORMERS



创新点:

- 提出DMA机制（融合特征）
  - 提出Dynamic Multi-level Attention mechanism (DMA) （ 优于类似大小的视觉转换器 (ViT) 和卷积神经网络 (CNN)）
- 提出DMFormer的高效骨干网
- DMA替换自注意力机制
- DMFormer替换vision transformer 的结构









DMA

- 多尺度扩张卷积
- 轻量级门控机制提供输入适应性



![image-20230407091520466](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230407091520466.png)


$$
V =  ReLU(FC(GAP(X))
$$

$$
Attn = Sigmoid(FC(V))
$$

$$
Output = Attn \bigotimes Conv1 \times 1(X')
$$













DMFormer

![image-20230407094559615](C:/Users/Administrator/AppData/Roaming/Typora/typora-user-images/image-20230407094559615.png)











数据集：

- ImageNet-1K
- ADE20K











这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 自注意力机制计算成本很高，很多人提出卷积运算代替视觉转换器中的自注意力机制，使用卷积的话内置归纳偏差更有效。但是使用卷积的话忽略了多层次特征and lack dynamic prosperity。transformer的自注意力机制计算成本很高 很难进行高分辨率的下游任务如语义分割。







这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

**相关研究：**

 

论文中提到的解决方案是什么，关键点在哪儿？



 直接用卷积替换Transformer不好，为此我们提出了DMA(动态多级注意力机制)

Dynamic Multi-level Attention mechanism

- 通过多个内核大小捕获输入图像的不同模式(DMA)(为不同的分辨率应用多个内核)
- 使用扩张卷积扩大感受野

- 通过门控机制启动输入自适应权重(DMA) （捕获通道关系并增强网络的表示能力）
  - 通过门控机制学习挑选信息特征
  - GAP获取全局信息 接两个FC最后sigmoid计算注意力向量
- 最后DMA输出的是通过门控机制校准的融合特征



提出DMFormer的高效骨干网络 替换注意力机制







论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

总体

![image-20230422111331289](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230422111331289.png)

其中Conv Steam 为 7x7 s = 2 3x3 s = 1 不重叠2x2 s = 2

DMAblock

![image-20230422111402740](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230422111402740.png)

DMA替换掉了自注意力



![image-20230422113017553](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230422113017553.png)



Imagenet分类 

- 300epoch
- 8 gpu
- total batchsize 1024
- 1e-3
- 用cosine decay schedule调整学习率



分类的Grad-CAM结果图

![image-20230422113025905](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230422113025905.png)





语义分割

ADE20k

mIoU衡量模型性能  FPN uperNet评估DMFormer-s骨干网的主要框架

- ImageNet1K 上的预训练权重用于初始化我们的主干。
-  我们使用 AdamW 优化器训练每个模型，在 8 个 GPU 上的总批大小为 16。 
- 当配备语义 FPN [21] 时，我们使用 [18、19] 中的 40K 迭代训练方案。
-  学习率设置为 2 × 10−4 并按幂为 0.9 的多项式衰减。
-  相比之下，我们为 UperNet 采用了 [3] 中的 160K 迭代训练方案。 具体来说，学习率设置为 6 × 10−5，迭代预热 1500 次，学习率线性衰减

![image-20230422113715821](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230422113715821.png)





消融实验

![image-20230422113758910](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230422113758910.png)





用于定量评估的数据集是什么？代码开源的话找到链接（细节）

**实验数据集：**

 ImageNet

 ADE20k







这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

**本文贡献：**

 





下一步还能基于它做什么？有什么工作可以继续深入？（宏观）