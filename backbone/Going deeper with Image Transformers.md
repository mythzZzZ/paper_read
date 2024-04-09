   ==Going deeper with Image Transformers==



we build and optimize deeper transformer networks for image classification

使用更深的网络处理图像分类 如何让更深的网络有更好的

提出的方法

- ==LayerScale==  
  - 我们在每个残差块的输出上添加一个可学习的对角矩阵，初始化接近（但不是）0。在每个残差块之后添加这个简单的层可以改善训练动态，使我们能够训练更深的高容量图像变换器 从深度中受益
- class-attention layers  CaiT
  - 更改了cls分类token的位置 先注意力后token
  - ![image-20230405093221187](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230405093221187.png)
