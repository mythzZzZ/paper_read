## QueryDet: Cascaded Sparse Query for Accelerating High-Resolution Small Object Detectio

QueryDet：用于加速高分辨率小物体检测的级联稀疏查询

2022 CVPR

小物体检测难的原因

- 由于卷积神经网络（CNN）主干中的下采样操作，突出显示小物体的特征被消除，因此，小物体的特征常常受到背景噪声的污染
- 低分辨率特征的感受野可能与[25]中指出的小物体的大小不匹配
- 定位小物体比定位大物体更困难，因为边界框的小扰动可能会导致交并集（IoU）度量的显着扰动
- 由于小物体在空间中通常稀疏（使用dia可以节省空间，更快的检测到），高分辨率特征图上的密集计算范式效率非常低（所以我们使用goolenet）（3.2）



解决小目标检测困难

- 使用大的特征图
- 重用特征
- 不同尺度的对象在不同级别上进行处理：大对象往往在高级特征上被检测到，而小对象通常在低级别上被检测到









这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

促进小目标检测最有效的方法

- 高分辨率图像
- 高分辨率特征图

- ==但是计算成本会随着图像和特征大小的增加呈正比增加==





论文中提到的解决方案是什么，关键点在哪儿？

小目标检测存在的问题

- 低级特征的计算高度冗余。 大多数情况下，小物体的空间分布非常稀疏：它们只占据高分辨率特征图的一小部分； 因此浪费了大量的计算量。 
- 特征金字塔是高度结构化的。尽管我们无法准确检测低分辨率特征图中的小物体，但我们仍然可以高置信度地推断它们的存在和大致位置。





 提出QueryDet（主要节省检测头的计算量）

- 它首先预测低分辨率特征上小物体的粗略位置，然后使用这些粗略位置稀疏引导的高分辨率特征计算准确的检测结果

- 我们不仅可以获得高分辨率特征图的好处，还可以避免对背景区域进行无用的计算
- 可以减少所有基于特征金字塔的对象检测器的计算成本。 我们的方法可以通过有效利用高分辨率特征来提高小物体的检测性能，同时保持快速的推理速度











![image-20230722101118227](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230722101118227.png)



我们递归地预测低分辨率特征图上小对象（查询）的大致位置，并使用它们来指导更高分辨率特征图上的计算











