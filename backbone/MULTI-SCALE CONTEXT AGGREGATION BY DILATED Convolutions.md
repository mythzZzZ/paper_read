==MULTI-SCALE CONTEXT AGGREGATION BY DILATED CONVOLUTIONS==

通过扩张卷积进行多尺度上下文聚合

​																												ICLR 2016



新的密集预测卷积网络模块 contextnetwork

- 使用扩张卷积
  - 扩张卷积支持以指数方式扩展感受野，而不会损失分辨率或覆盖范围

- 可以在不丢失分辨率或分析重新缩放的图像的情况下聚合多尺度上下文信息



![image-20230411082019426](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230411082019426.png)



- 前7层为context network 第八层恢复通道c 
- 6->7没有指数增长，输入的尺寸为64，此时感受野已经65了





dilated convolutions

- dilated =1，2，4，8         dilated指数形式扩张



![image-20230411090354293](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230411090354293.png)



![image-20230411090401884](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230411090401884.png)

提出两个新的模块

- front-end （去掉原有的分类模块）
  - 改输入图片的尺寸为 64x64
    - 反射填充
  - 把 c = 3 -> c = 21
- context network

