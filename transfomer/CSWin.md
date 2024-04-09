==CSWin Transformer: A General Vision Transformer Backbone with Cross-Shaped Windows==

==论文创新==

1.新的计算窗口注意力的方法：

-  CrossShaped Window self-attention
  - 用于并行计算形成十字形窗口的水平和垂直条纹中的 self-attention，每个条纹都是通过将输入特征分成等宽的条纹获得的。



2.LePE位置编码

- 更好处理局部位置信息
- 支持任意输入分辨率









==数据集==

- coco
- ImageNet-1K
- ADE20K











==CrossShaped Window self-attention==

- 条状的注意力窗口计算注意力
  - Multi-heads分两组(并行计算)
    - 水平条
    - 竖直条
- 沿着网络深度增加条带宽度，以进一步扩大注意力区域，同时增加微妙的额外计算成本

- 计算注意力
  - ![image-20230405170114173](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230405170114173.png)
  - X被均匀地划分为等宽sw的非重叠水平条纹[X1, .., XM]
  - 每一条计算attention
  - k为第k个头  $d_k$ 的值 C/K
- 一共k个头分成两组  
  - 水平条
  - 竖直条
  - 做完注意力两组拼接
  - ![image-20230405171026683](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230405171026683.png)



















==LePE位置编码==

- ![image-20230405163500957](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230405163500957.png)
- 在attention计算的时候在v矩阵中加入位置编码





问题。每个头的dim









Cvt: Introducing convolutions
to vision transformers

















