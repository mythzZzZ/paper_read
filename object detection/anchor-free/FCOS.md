# FCOS: Fully Convolutional One-Stage Object Detection



anchor-Free



这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 ![image-20230707160656237](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707160656237.png)







论文中提到的解决方案是什么，关键点在哪儿？



无需定义框的尺寸，直接预测中心点坐标和中心点距离目标四周的四个距离，通过中心点和四边的四个距离得到anchor

![image-20230707162326455](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707162326455.png)

公式中的s是特征图相对于原图的步距

$x_{min} y_{min}是左上角的坐标  x_{max} y_{max}是右下角的坐标$ 





![image-20230707163027207](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707163027207.png)



Center-ness描述距离目标中心的远近程度

根据公式   0<Center-ness<1        

- 当预测点在中心时  $l^*  =  r^*$ 此时Center-ness = 1
- 当预测点在边界时 Center-ness = 0





anchor-free的正负样本匹配

![image-20230707164346960](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707164346960.png)



取sub-box里面的点为正样本

- sub-box左上角，右下角的坐标分别为（cx - rs,cy-rs,cx+rs,cy+rs）
- grid cell要在sub-box范围内才为正样本
- 一个feature map内不是正样本其余都为负样本







Ambiguity问题，当预测点落入到多个目标的GT相交区，预测点要如何分配呢

![image-20230707164654916](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707164654916.png)

- 默认分配给面积rea最小的GT Box







损失计算

![image-20230707165127571](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707165127571.png)

center-ness只计算正样本的损失







![image-20230707170003815](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707170003815.png)

- 低层的特征图适合预测小目标 （低层特征图保存更多的细节信息）
- 高层的特征图适合预测大目标



