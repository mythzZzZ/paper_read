==ConvNeXts==

==让人们重新思考卷积的重要性==



transformer架构选择可以合并到ConvNet中

- 提出传统的ConvNet和视觉Transformer之间的性能差异很大一部分可能是由于训练技巧

- 模型的结构





transformer的可扩展性是什么







ConvNexts

- 特别的训练过程(现代化的优化技术) 

  - 主要与优化策略和相关的超参数设置有关
  - AdamW优化器
  - 数据增强
  - Mixup , Cutmix , RandAugment , Random Erasing , and regularization schemes including Stochastic Depth [36] and Label Smoothing 都用在训练网络上

- AdamW优化器（迭代次数 90 epochs -> 300 epochs）

- 优化阶段计算比率（stage ratio）

  - 如transformer的每个模块对比为1:1:3:1
  -  ResNet-50 中的 (3, 4, 6, 3) 调整为 (3, 3, 9, 3) 

- patchify strategy(处理图片的输入)

  - swin的patch为4x4 参考改ResNet的输入卷积

  - 使用4x4 步为4的卷积代替 7x7 步长为2的卷积

- 使用深度卷积 且 增加网络的宽度(隐藏层的数量) 和 swin-T一样相同的通道数(64 -> 96)

- Inverted Bottleneck()
  - the hidden dimension of the MLP block（把MLP输入维度变成原来的四倍宽）
- Large Kernel Sizes (大卷积核 增加全局感受野)
  - swin 采用7x7窗口注意力块 ResNet为3x3
  - 改变dw卷积核为7X7 dw位置上移（depthwise convolution 类似于 self-attention 中的加权求和操作）
- Micro Design 网络设计的小改动
  - 改激活函数
  - 减少激活函数
  - 更少的norm层
  - 用 LN代替BN(LN与BN的区别 )
  - Separate downsampling layers（单独的下采样）
    - ResNet的空间下采样用残差块实现的改为单独下采样层using 3×3 conv with stride 2 (and 1×1 conv with stride 2 at the shortcut connection)
    - 在空间分辨率发生变化的地方添加归一化有助于稳定训练
    - 在下采样之前添加LN层





transformer特别的训练技术

- AdamW优化器
- patchify strategy





stage compute ratio：阶段计算比率

例如 Encoder阶段 Decoder阶段 Output阶段



Macro Design:宏观设计

stem cell:模型的基础结构

- 处理输入图像的模块

Inverted Bottleneck

- 受transformer块的影响 MLP块的隐藏维度比输入比输入维度宽四倍



![image-20230331103326446](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230331103326446.png)







增大全局感受野

- 大卷积核
- VGGNet推广：堆叠3x3的卷积









![image-20230331170436274](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230331170436274.png)

4个圆代表4维



![image-20230331170521775](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230331170521775.png)



![image-20230331170531602](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230331170531602.png)