yolov5四个版本



**Yolov5s、Yolov5m、Yolov5l、Yolov5x**

[yolov5](https://zhuanlan.zhihu.com/p/172121380)

[v5](https://blog.csdn.net/qq_37541097/article/details/123594351)

这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 v4缩放图像黑边大，像素会影响，速度更慢







这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

相关研究：

 

论文中提到的解决方案是什么，关键点在哪儿？

 

![image-20230516092819199](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230516092819199.png)





#### 输入端的优化

**Mosaic数据增强**



 **自适应锚框计算**



 **自适应图片缩放**（让v5速度加快）

- V5缩放图像时 添加了更少的黑边，使填充像素影响更少，推理时间更快（37%的提升）





#### Backbone的优化



- 新增**Focus结构**（v4没有）

![image-20230516094153226](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230516094153226.png)



- 2个csp结构(v4一个csp结构)

![image-20230516094558731](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230516094558731.png)







#### NECK优化

![image-20230516094740416](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230516094740416.png)



![image-20230516094819846](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230516094819846.png)



- yolov4的neck只采用了卷积，没有加入csp结构
- v5的neck中加入了csp架构









#### 输出端

- Yolov5中采用其中的CIOU_Loss做Bounding box的损失函数(和4一样)

- **nms非极大值抑制**

- Yolov4在DIOU_Loss的基础上采用DIOU_nms的方式，而Yolov5中采用加权nms的方式











论文中的实验是如何设计的？各个实验分别得到了什么结论？（细节）

 

用于定量评估的数据集是什么？代码开源的话找到链接（细节）

实验数据集：

 

这篇论文到底有什么贡献？（三句话内说明）新在什么地方？（宏观）

本文贡献：

 

下一步还能基于它做什么？有什么工作可以继续深入？（宏观）