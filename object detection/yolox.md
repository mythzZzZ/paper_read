# YOLOX: Exceeding YOLO Series in 2021



2021 CVPR





这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 升级 YOLO，在参数量相同的情况下提升了AP



anchor机制的坏处

- 聚类得到最好点 不太普遍
- anchor机制增加了检测头的复杂度，每幅图像的预测数量，在某些边缘设备上可能会存在整体延迟
- 







这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

相关研究：

 

论文中提到的解决方案是什么，关键点在哪儿？

 

与传统yolo的不同点，yolox加入的东西

- anchor-free （减少参数量）
- 其他高级检测技术
  - decoupled（解耦头） 不同的头使用的loss不一样
  - SimOTA（领先的标签分配策略 正负样本匹配）











什么是解耦头？

问题：如果采取用同一个特征图进行分类和定位，效果会不好，即所谓的misalignment的问题

提出解耦头来解决这个问题

- 提出利用不同的头来分类和定位 （速度更快）

- 传统的yolo特征金字塔每个特征图后直接输出 c = anchor * (5+class)
- 解耦头：FPN特征 -> 1x1 改变通道为256->输出三个分支进行不同的任务





![image-20230524111442074](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230524111442074.png)



![image-20230524115342278](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230524115342278.png)





Anchor-Free

![image-20230707173306470](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707173306470.png)

- 每个grid-cell都会预测四个位置参数 $t_x t_y t_w t_h$  

- 其中 $t_x t_y$  加上 $c_x c_y$ 可以得到中心点的坐标，这个中心点的坐标也是anchor中心点的坐标
- $e^{t_w} e^{t_h}$ 分别是anchor方框的w和h







损失计算

![image-20230707173903224](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707173903224.png)







正负样本匹配SimOTA

![image-20230707174256235](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707174256235.png)



![image-20230707174444527](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707174444527.png)





如何分配正样本

![image-20230707174620526](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707174620526.png)

- 首先寻找GTbox里面的所有 fixed center area （类似于fcos中的sub-box）
-  fixed center area中被选中的gridcell为正样本
-  在GT里面不是正样本的点就是负样本





![image-20230707175052172](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707175052172.png)

anchor point首先选取fixed center area里面的点，如果不够在选取fixed center area外的点（这些点必须在GT里面）





计算每个GT要分配 Anchor point的个数（GT要分配给哪个grid cell的个数）

![image-20230707175522615](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707175522615.png)

- 得到每个标签要分配的grid-cell个数







![image-20230707175910135](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707175910135.png)

得到anchor-point的个数后，从上面的表中选取cos最小的那几个构造分配矩阵

分配矩阵如上图 下面的表所示，此时对应的位置 置1了

- 此时A5分配给了两个GT 如何解决这个问题？

  - 对比两个GT的cos，此时要选择cos较小的GT
  - ![image-20230707180310367](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230707180310367.png)

  ​      得到最终的分配矩阵表如上图第二个表所示，此时分配矩阵里面为1的为正样本，其他为负样本

  ​     （）

