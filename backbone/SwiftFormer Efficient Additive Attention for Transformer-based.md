SwiftFormer: Efficient Additive Attention for Transformer-based Real-time Mobile Vision Applications



2023 CVPR





这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 自注意力机制的矩阵乘法运算复杂度很高，这篇论文引入了新的高效注意力机制。







论文中提到的解决方案是什么，关键点在哪儿？



 引入了新的高效加法注意力机制

-  该机制有效地用线性逐元素乘法代替了二次矩阵乘法运算
  - 可分离的自注意力机制，将矩阵乘法运算替换为逐元素乘法
- 不牺牲任何准确性的情况下用线性层替换键值交互
- 我们有效的自注意力公式使其能够在网络的所有阶段使用

- 线性自注意力:高分辨率(网络初期)使用卷积，网络后期使用transformer
  - 我们提出的高效注意力设计可用于网络的所有阶段，从而实现更有效的上下文信息捕获并实现卓越的速度-准确性权衡





![image-20230604094649395](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230604094650109.png)





### 逐元素乘法注意力与高效additive注意力



![image-20230604110336773](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230604110336773.png)



传统空间维度注意力
$$
att = Softmax(\frac{Q \cdot K^T}{\sqrt{d}}) \cdot V
$$


Transpose Self-attention （使用特征图进行自注意力）
$$
att = V \cdot Softmax(\frac{Q^T\cdot K}{\sqrt{d}})
$$


逐元素乘法自注意力

查询 (Q)、键 (K) 和值 (V) 之间的交互使用逐元素操作进行编码。首先，查询矩阵 Q 被投影为一个维度为 n × 1 的向量 q，然后输入 Softmax 以生成上下文分数，它捕获每个查询元素的重要性。 然后，将上下文分数乘以矩阵 K 并合并以计算上下文向量，该向量对上下文信息进行编码。 最后，上下文向量与值矩阵 V 逐元素相乘以传播上下文信息并产生最终输出。



*表示逐乘法运算


$$
att = V * \sum K * Softmax(q)
$$




NLP 中典型的附加注意机制通过逐元素乘法而不是使用点积运算来利用标记之间的成对交互来捕获全局上下文。

实验表明可以在不牺牲性能的情况下删除键值交互，并且仅通过合并线性投影层专注于有效编码查询键交互就足以学习标记之间的关系. 这种方法称为高效加法注意





### Efficient Additive Attention



![image-20230604104552562](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230604104552562.png)





1.输入x经过$w_q w_k$矩阵得到Q K矩阵

2.查询矩阵 Q 乘以可学习参数向量 $w_a$​ 以学习查询的注意力权重，然后进行 Softmax 操作以产生全局注意力查询向量 α
$$
a = \frac{exp(Q \cdot W_a / \sqrt d)}{\sum_{j=1}^n exp(Q \cdot w_a / \sqrt d)}
$$


3.查询向量加起来得到全局查询向量
$$
q = \sum ^n_{i=1}a_i * Q_i
$$
4.K矩阵与向量q相乘，得到全局上下文



5.linear(全局上下文)与linear(Q)相加得到结果
$$
att = \hat{Q} + T(K * q)
$$








###  SwiftFormer Architecture



![image-20230604112212933](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230604112212933.png)









论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

imagenet-1k （使用了蒸馏）

首先在EfficientFormer模型上替换自己的模块进行实验

![image-20230604112956499](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230604112956499.png)



自己的模型与其他模型比较

![image-20230604113135498](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230604113135498.png)



![image-20230604113550352](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230604113550352.png)



MS-COCO



ADE20K



 

下一步还能基于它做什么？有什么工作可以继续深入？（宏观）