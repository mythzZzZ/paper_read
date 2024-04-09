使用 Darknet-53为主干网络，主干网络加上好的头，就是一个好的目标检测网络



![image-20230511101132574](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230511101132574.png)





![image-20230511104710438](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230511104710438.png)

















这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 

解决传统yolo对小目标检测效果比较差的问题(若图像中有很多个物体，框不能全都检测出来)





这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

相关研究：

 



论文中提到的解决方案是什么，关键点在哪儿？

 

提出了多尺度的检测，输出三个出的的特征

- c=255 每个块画三个anchor，使用coco数据集训练 检测80个类别。255 = 3 x（4+1+80） 这个1为objectness （该框内有对象的概率）
  
- 多尺度  HXW越大 感受野越小

![image-20230511101408028](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230511101408028.png)



 





为什么要多尺度呢

- 每个尺度的预测框的大小不一样
- HxW越小 anchor的尺寸就越大 （此时负责预测大物体）图1蓝
- HxW越大 anchor的尺寸就越小 （此时负责预测小物体） 图2，3 蓝色



![image-20230511103832091](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230511103832091.png)





三个尺度 一共的预测框数为  13x13x3 + 26x26x3 + 52x52x3





损失函数

![image-20230511105652952](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230511105652952.png)





得到三个特征图，转化成输出的结果

![image-20230511110003812](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230511110003812.png)









![image-20230511111756285](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230511111756285.png)





论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

用于定量评估的数据集是什么？代码开源的话找到链接（细节）

实验数据集：

 

这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

本文贡献：

 

下一步还能基于它做什么？有什么工作可以继续深入？（宏观）