yolov2





这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

  v1的缺点

- map比较低
- recall比较差（把图片上所有目标都检测出来）
- 7x7个块 最多检测49个目标 对小目标检测的能力比较差











这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

相关研究：

 

论文中提到的解决方案是什么，关键点在哪儿？

 better

- Batch Normalization
- High Resolution Classifier  高分辨率分类器 （现在224先224上训练分类一会 在使用448x448图像训练分类）
- Anchor   Dimension Cluster(聚类选anchor)     Direct location prediction （每个块给很多初始框 初始框的形状通过聚类算法得到，然后预测框的偏移量  v2把图像画成13x13块 每个块5个anchor）
  - ![image-20230510094836634](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230510094836634.png)

​			每个anchor 4个位置信息 一个置信度 20个类别信息 一共25个数

​			每个块5个anchor 所以每个块有 125个数  c =125  ouput = 13x13x125

​		125 （一个anchor预测一个类别，类别信息在anchor里面）

预测偏移量![image-20230510100111339](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230510100111339.png)



损失函数

![image-20230510100614368](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230510100614368.png)





 

- Fine-Grained Features 细粒特征

![image-20230510101942686](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230510101942686.png)



原图经过卷积 与 原图分成四块(patch embedding)拼起来相加 使高纬度与低纬度的特征相互融合。



![image-20230510103514934](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230510103514934.png)









- Muti-Scale Training  多尺度训练



![image-20230510104004421](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230510104004421.png)



 使用全局池化 代替 FC

- 输入尺度大 精度大  速度慢
- 输入尺度小 精度小  速度快



![image-20230510104343309](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230510104343309.png)







Faster（更换了backbone）

- 使用Darknet19 （使用1x1卷积）



左边分类网络 右边检测网络

![image-20230510104607964](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230510104607964.png)







stronger（类别更多）

- 开脑洞（并没有实际训练出来 ）



![image-20230510105725004](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230510105725004.png)









 

v1类别信息在cell里面 两个box预测同一个类别，v2的类别信息在anchor里面，每个anchor可以预测一个类别





