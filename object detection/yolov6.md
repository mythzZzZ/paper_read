YOLOv6: A Single-Stage Object Detection Framework for Industrial Applications

YOLOv6：用于工业应用的单级目标检测框架













这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）



以前的yolo模型放在工业实际场景可能被不太行

- 计算资源受限
- 网络架构比较大





论文中提到的解决方案是什么，关键点在哪儿？



创新点

YOLOv6 的改造设计包括以下组件

- 网络设计,小模型单路径结构
- 标签分配
- 损失函数
- 数据增强
- 行业便利的改进以及量化和部署
- 知识蒸馏，多训练时期
- anchor-free



backbone

- RepVGG （在推理小模型的时候有更多的特征表示能力）
  -  RepVGG重新参数化技术称为()
- 使用RepBlock作为小型网络的构建块
- 该模型的大模型版本使用CSPStackRep block (修改后的csp块)



neck

- neck采用PAN结构

- 使用 RepBlocks 或 CSPStackRep Blocks 增强颈部以拥有 RepPAN



head

- 简化decoupled head使其更高效，称为Efficient Decoupled Head
  - 使用混合通道解耦策略



标签分配策略 **

- TAL（Task alignment learning）



损失函数

- VariFocal Loss 分类损失
-  SIoU [8]/GIoU Loss 作为我们的回归损失。



![image-20230607093851242](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607093851242.png)





RepBlock



![image-20230607094418380](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607094418380.png)



a:		RepVGG block

b:		RepConv 表示在推理时候的RepVGG block

c:		CSPStackRep Block











论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 先于其他模型作对比

![image-20230607102925267](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607102925267.png)





自身消融实验，Relu激活函数消融

- 当涉及到工业应用时，尤其是部署具有 TensorRT [28] 加速的模型时，ReLU 因其融合到卷积中而具有更大的速度优势、

![image-20230607103316573](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607103316573.png)



neck的宽度（channel)消融

![image-20230607103916081](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607103916081.png)





使用不同卷积与与激活函数的消融

![image-20230607103729016](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607103729016.png)





Loss消融

![image-20230607105001044](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607105001044.png)





![image-20230607105305620](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607105305620.png)





epoch 消融

![image-20230607110343646](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607110343646.png)



蒸馏消融

![image-20230607110353663](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607110353663.png)





数据增强消融

![image-20230607110536574](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230607110536574.png)





这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

本文贡献：

 

下一步还能基于它做什么？有什么工作可以继续深入？（宏观）