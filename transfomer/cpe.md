CONDITIONAL POSITIONAL ENCODINGS FOR VISION
TRANSFORMERS



绝对编制编码

- 传统的绝对位置编码成用在长序列的时候要插值
- 图像移动的时候输出的特征图会变(平移等变性)，采用绝对位置编码时破坏了这个特性





conditional positional encoding (CPE)

- 有条件的位置编码（相对位置）

Position Encoding Generator (PEG)

- 编码生成器

Conditional Position encoding Vision Transformer (CPVT)

- 有条件的位置编码视觉转换器



CPE的优势 

- 是动态生成的，并以输入标记的局部邻域为条件

- 可以为更长的序列编码
- 在transformer的encode中整合相对位置编码
- 具有平移等变性



==PEG的实现过程==

![image-20230329155207108](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230329155207108.png)



- 向量token还原为图像
- 图像patch经过F函数获得cpe(条件位置编码)

![image-20230329161040325](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230329161040325.png)

[PEG框架](https://zhuanlan.zhihu.com/p/373581699)

F函数是一个2d卷积