总体流程 

特征提取 -》分配标签 -》计算损失





### v1 



2016CVPR



==主干==



==标签分配==

- 图像的中心落入到某个网格中，这个网格负责预测目标
- 每个网格预测B个bounding box(boundingbox里面网格预测位置信息，confidence)，类别分数
  - 7x7(2x5 + 20)   2x5为两个bbox 每个box里面5个信息
- 位置信息中心坐标(x,y)相对于grid cell 左上角而言的相对坐标, 宽和高相对于整个图像而言

- confidence = Pr(object) * IOU （该box存在对象的 IOU）



==计算损失==

bounding box 损失+  confidence损失   + classes损失

- bounding box 计算损失不能直接减，因为大小目标偏差会不一样，直接减小目标的偏差会更大，所以计算损失的时候利用开根号的减



![image-20230614103918265](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230614103918265.png)

 



![image-20230614103908273](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230614103908273.png)



缺点

- 检测不了很多目标，小目标
- 出现新的目标尺寸 预测效果差
- 定位不准确(直接预测目标信息)







### v2

2017CVPR



==主干==

Darknet-19





grid cell  13X13

使用科技

- BN层 卷积层后加BN (防止过拟合 正则化处理 帮助收敛 使用BN层移除dropout)
- High Resolution Classifier  高分辨率的分类器 (更大的图片输入尺寸 448 X 448)
- Anchor Boxes 预测方式 目标边界框预测 每个cell5个anchor
- Dimension Clusters        anchor的聚类 初始化画anchor的尺寸 使用k-means聚类获取尺寸
- FIne-Grained Features    对不同的特征层进行信息融合
  - 高维度特征与低纬度特征 特征相同的位置conca


- 多尺度训练 不同尺度的图像训练网络 （每10个epoch对输入图片尺寸进行随机选择）



==标签分配==

边界框预测

- 让anchor 预测相同grid cell里面的目标





给预测框分配标签计算损失





==计算损失==









### v3



==主干==



Darknet-53









==标签分配==

- 每个cell 3个anchor  n x n x 3 x (85) 每个anchor 里面包含4个位置信息 一个置信度 80个类别信息(coco)



目标边界框预测

![image-20230614163215404](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230614163215404.png)

每个cell的范围是 0-1  sigmoid($t_x$) 把当前cell里面anchor坐标限制在0-1，此时这些anchor得到相对于左上角的相对坐标，同时也确定该object的预测框是从当前cell中选取



**每个GT分配一个正样本**

- 选取与GT重合度最高的为bbox为正样本(只选取一个)，若大于某个阈值却不是重合度最高的，这些样本既不是正样本也不是负样本此时这些样本直接丢弃，少于某个阈值的是负样本
- 若bbox不是正样本，则这些bbox只有 objectness损失







​                                                                                                                                                                                                                                                                                                                                                                                                                                               



==计算损失==



![image-20230614171605439](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230614171605439.png)



置信度损失:二值交叉熵损失

![image-20230614171701515](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230614171701515.png)



绿色是GT  蓝色是BBox   把预测的目标边界框偏移量应用到BBox上，让蓝色移动(改变蓝色的中心坐标)得到黄色的目标边界框，此时黄色的边界框为预测边界框  （偏移量怎么得到呢？通过损失函数 不断训练网络 迭代）





类别损失：二值交叉熵损失

![image-20230614172824735](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230614172824735.png)



![image-20230614173103349](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230614173103349.png)



定位损失

![image-20230614173313801](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230614173313801.png)







==v3-SPP==



![image-20230615102435282](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615102435282.png)



![image-20230615104135315](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615104135315.png)

#### ==IOU==

![image-20230615104335321](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615104335321.png)



#### ==GIoU==

![image-20230615104419518](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615104419518.png)

U为重合的面积  $A^C$ = 包裹外框的面积

当两个框重合时U=1 $A^C$ = 1  重合时IOU = 1   此时GIOU = IOU = 1

当两个框无穷远时   U = 0  此时 GIOU = IOU - 1 无穷远时 IOU = 0 此时 GIOU = -1





#### ==DIOU==

![image-20230615110618259](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615110618259.png)

GIOU不好解决重合问题





![image-20230615110751847](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615110751847.png)

d为两个点中心距离，C为外接矩形的对角线长度





#### ==CIOU==

![image-20230615111457684](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615111457684.png)







Focal loss

负样本较多的情况

![image-20230615113038407](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615113038407.png)



![image-20230615115253807](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615115253807.png)













### v5



==主干==



![image-20230615154950089](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615154950089.png)

![image-20230615155130248](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615155130248.png)



数据增强

- Mosaic 四张图片拼成一张
- Copy paste 把a图的图像抠出来放到b图 （数据里里面有实例分割的标签）
- Random affine 随机仿射变换 （随机平移旋转缩放错切）
- Mix up  几张图片按照不同的透明度放在一起

- Albumentations （滤波、直方图均衡化以及改变图片质量）

- Augment HSV（Hue，Saturation，Value）色度、饱和度、明度



训练策略

- Multi-scale training(0.5~1.5x) 多尺度训练 图像尺寸在 0.5-1.5中随机取值去32的整数倍  下采样最后得到的是32的整数倍
- AutoAnchor (For training custom data) 重新聚类生成新的anchor尺寸
- Warmup and Cosine LR scheduler (学习率从小慢慢增大到我们设置的学习略 相对于热身)
- EMA （Exponential Moving Average）给变量加上动量 更新参数的时候更加平滑
- Mixed  precision 混合精度训练 减少GPU显存的占量 （减少一般显存 理想状态加速两倍）
- Evolve hyper-parameters （进化超参数）







==标签分配==



总结思路  分配标签 -> 获取正样本 ->计算IOU

- 先把GT与anchor进行计算，计算出GT分配给第几个anchor （v5是 GT包住0.5倍anchor，4倍anchor包住GT则匹配成功）
- GT回到自己的cell，然后通过可以走多长的偏移量，选择哪几个cell的anchor为正样本预测框
- 得到多个正样本后与GT计算IOU和偏移量（GIOU），得到GIOU最小的预测框用来计算损失
- 最终不同尺度对应GT都会有一个预测框，对每个尺度的框进行后处理最后得到一个框





==计算损失==



![image-20230615161656289](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615161656289.png)



![image-20230615162145498](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615162145498.png)

之前的IOU计算如上图，如果当预测点坐标在边界上时  此时$b_X  =  C_X  或 b_y = C_y$ 此时 需要 $\sigma(t_x) = 0 或 \sigma(t_y) = 0$  由于 $\sigma(x)$的方程 此时需要 x取无穷值，所有存在不合理的地方



此时引入一个缩放因子

![image-20230615162740181](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615162740181.png)



方框 W H的计算

![image-20230615163040572](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615163040572.png)





正样本的匹配

![image-20230615163428476](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615163428476.png)

如果GT 在anchor 的0.5-4倍的范围内 就匹配成功  把GT模板分配给anchor 2 和3



![image-20230615165025163](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230615165025163.png)

把GT分给他所在的cell 由于预测坐标得偏移量为0.5~1.5 他上边的cell和左边的cell都可以匹配到这个GT 此时选取上边的cell和左边的cell的第几个anchor为正样本



