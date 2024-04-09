==MixConv: Mixed Depthwise Convolutional Kernels==



==MixConv:单个深度卷积中混合多个内核大小代替普通深度卷积(结合多个dw卷积核让他更有效)==

更合理设置dw的卷积核大小





==MixConv==

单个dw内核：

- 不能捕获更多的特征
- 

多个dw内核：

- 大内核捕获高分辨率特征
- 小内核捕获低分辨率特征
- 给输入图像的通道分组 不同的组用不同的卷积核大小

多内核如何划分

输入图片c怎么分组

- 均分   input:32 group：4  (8:8:8:8) 
- 指数分 第i组  C * $2^{-i}$  （16，8，4，4） 最后一组用剩下的

- 每组内核大小递增2(从3x3开始 3x3具有较少的参数)



![image-20230502104906531](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230502104906531.png)







提出==MixNets模型==：

- 移动端模型
- 作对比的模型
  - MobileNet  ShuffleNetV2 MnasNet   ProxylessNAS   FBNet



























数据集

- COCO
- ImageNet