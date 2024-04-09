CYCLEMLP: A MLP-LIKE ARCHITECTURE FOR DENSE PREDICTION

​																							2021 CVPR



MLP无注意力架构可以作为通用视觉主干



传统的MLP架构与图像大小相关，因此在对象检测和分割中不行。我们提出了CycleMLP

CycleMLP

- 可以应对各种图像尺寸
- 通过使用局部窗口实现了图像尺寸的线性计算复杂度















这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）


 传统的MLP架构与**图像大小相关**，因此在对象检测和分割中不行。我们提出了CycleMLP (MLP无注意力架构可以作为通用视觉主干)

传统MLP架构

(1))当前模型由具有非层次结构的块组成 ，这使得模型无法提供金字塔和高分辨率特征表示。

(2) 由于空间 FC，当前模型无法处理灵活的输入尺度， 结构通常需要在训练和推理过程中具有固定比例的输入图像。 它与密集预测任务的要求相矛盾，后者通常采用多尺度训练策略 (Carion et al., 2020) 以及在训练和推理阶段采用不同的输入分辨率 (Lin et al., 2014; Cordts et al., 2016) .

 (3) 当前 MLP 模型的计算和内存成本与密集预测任务的输入图像大小成二次方（例如，COCO 基准（Lin 等人，2014 年））。



CycleMLP

- 可以应对各种图像尺寸(造金字塔结构)
- 通过使用局部窗口实现了图像尺寸的线性计算复杂度(循环全连接层（Cycle FC）)
  - ![image-20230426091612734](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426091612734.png)









这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

**相关研究：**

 MLP:使用无注意力MLP主干可以进行视觉任务







论文中提到的解决方案是什么，关键点在哪儿？



 一、提出了一个新的FC方法

（1）channel FC 线性复杂度 可以处理各种输入维度 但是没有Spatial FC的感受野

（2）Spatial FC 具有全局感受野 参数大小固定 复杂度高 是输入图像的二次计算复杂度

（3）Cycle FC

- 具有channel FC的复杂度和比channel FC更大的感受野
- ![image-20230426092842275](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426092842275.png)
- ![image-20230426111335576](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426111335576.png)
- ![image-20230426110501270](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426110501270.png)



 二、利用该FC方法建立了一个MLP架构







 

论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

![image-20230426094536395](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426094536395.png)



模型结构

![image-20230426101615676](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426101615676.png)





![image-20230426101822715](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426101822715.png)



1.通道FC 空间FC与 循环FC的比较



2.循环FC与 self attention比较



PVT-style 中的模型命名为 CycleMLP-B1 至 CycleMLP-B5，Swin-Style 中的模型命名为 CycleMLP-T、-S 和 -B，



分类 ImageNet

![image-20230426103636360](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426103636360.png)



![image-20230426103138492](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426103138492.png)

分类的消融实验



![image-20230426103624631](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426103624631.png)





目标检测 coco



![image-20230426103515909](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426103515909.png)



实例分割

![image-20230426103807142](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426103807142.png)



语义分割  ADE20K



![image-20230426103917534](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426103917534.png)





![image-20230426104044593](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426104044593.png)





鲁棒性

![image-20230426104158113](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426104158113.png)





结构对比

![image-20230426104504358](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426104504358.png)



![image-20230426113112486](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230426113112486.png)

用于定量评估的数据集是什么？代码开源的话找到链接（细节）

**实验数据集：**



分类 ImageNet

目标检测 coco

语义分割  ADE20K



篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

**本文贡献：**

 







下一步还能基于它做什么？有什么工作可以继续深入？（宏观）