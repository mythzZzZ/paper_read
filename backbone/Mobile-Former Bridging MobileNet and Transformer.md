### Mobile-Former: Bridging MobileNet and Transformer





融合MobileNet 和 Transformer

- MobileNet获得局部特征 与T获得的全局特征融合
- MobileNet在本地处理中有很高的效率 节约计算成本



模型结构



![image-20230419100433421](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230419100433421.png)





![image-20230419100418839](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230419100418839.png)





双向桥的MobileNet

- 图片作为输入



双向桥的Former

- 可学习的参数（token）作为输入 （这些token是随机初始化的）
  - Former相对比与vit有更少的token  每个token代表图像的全局信息





核心： A light-weight cross attention

- 让attention的qkv来自于两个不同的分支

















































































==这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）==

 出现了很多conv与T的结合 都是串行的 还没有并行的 它弄了个并行的出来

这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

==**相关研究：**==  swin  vit  关于T的模型

 

==论文中提到的解决方案是什么，关键点在哪儿？==

 使用并行的mobileNet和T的结构  

 关键点

- 这样的结构可以有效的减少参数量 节约计算资源
- 并行运算 一边全局特征 一边局部特征 然后融合

==论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）==

 

==用于定量评估的数据集是什么？代码开源的话找到链接（细节）==

**实验数据集：**

 ImageNet

COCO





==这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）==

**本文贡献：**

 

==下一步还能基于它做什么？有什么工作可以继续深入？（宏观）==