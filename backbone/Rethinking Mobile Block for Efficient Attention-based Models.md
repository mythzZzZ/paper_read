# Rethinking Mobile Block for Efficient Attention-based Models

2023 CVPR



本文对轻量化模块进行研究，Inverted residual Block(IRB)倒残差结构的出现没有被基于注意力的研究所认可，作者从统一的角度重新思考高效 IRB 和 Transformer 的有效组件的轻量化研究，作者推导了一个现代的倒置残差移动块 (iRMB)，并构建了一个仅使用 iRMB 的 ResNetlike 高效模型 (EMO) 用于下游任务。







IRB

![image-20230531091205090](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531091205090.png)







这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 传统的cnn倒残差结构是一种非常高效的结构，但是受限与CNN固有的归纳偏差，纯CNN模型准确率仍然保持较低的水平，作者基于注意力模块构建了一个轻量级的类似IRB的基础模块。



![image-20230531093657701](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531093657701.png)









 

论文中提到的解决方案是什么，关键点在哪儿？



 作者基于注意力模块构建了一个轻量级的类似IRB的基础模块，从统一的角度重新思考 MobileNetv2 [51] 中的高效 Inverted Residual Block 和 Transformer [63] 中的有效 MHSA/FFN 模块，期望在基础模块设计层面整合两者的优势



![image-20230531094309782](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531094309782.png)

 



作者首先从当前模块发现模块的规律

![image-20230531160331697](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531160331697.png)



首先放大Channel 然后做处理  然后恢复Channel 最后残差相加



####  iRMB



该模块由 DW-Conv和EW-MHSA组成分别对短距离/长距离依赖进行建模



![image-20230531150527532](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531150527532.png)





 DW-Conv





EW-MHSa（MHSA 多头自注意力）



Q=K=X (∈ R C×H×W )，而扩展后的 值 Xe 为 V ( λC×H×W )。 这种改进被称为扩展窗口MHSA（EW-MHSA）

- 这种方式可以提高感受野的扩展速度





首先把这个模块用到其他模型，发现其他模型的性能提升

![image-20230531161554774](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531161554774.png)















#### EMO模型

(一个仅使用 iRMB 的 ResNetlike 高效模型 (EMO))

![image-20230531161917538](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531161917538.png)



模型参数

![image-20230531162354322](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531162354322.png)



该模型在imagenet-1k的消融实验

![image-20230531162717088](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531162717088.png)











论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

分类实验

训练参数

![image-20230531163024096](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531163024096.png)



实验对比结果

![image-20230531163211890](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531163211890.png)



在imagetnet-1k 不同stage的参数

![image-20230531163737467](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531163737467.png)





模型各模块所占的参数量

![image-20230531164158955](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531164158955.png)





特征图可视化



![image-20230531164258059](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531164258059.png)



将stage-3中具有不同组成的对角线像素的相似性可视化，DW-Conv往往具有短距离相关性，而EW-MHSA带来更多的长距离相关性。iRMB 利用了两个具有更大感受野的模块，即距离较远的位置具有较高的相似性。









部署在边缘设备上的实验

![image-20230531163516294](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230531163516294.png)





用于定量评估的数据集是什么？代码开源的话找到链接（细节）

实验数据集：

 

这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

本文贡献：

 

下一步还能基于它做什么？有什么工作可以继续深入？（宏观）



















