yolov4



[网络讲解](https://blog.csdn.net/qq_37541097/article/details/123229946)







这篇论文要解决什么问题？要验证一个什么科学假设？（宏观）

 

这篇论文有哪些相关研究，这些研究是怎么分类的？有哪些研究员值得关注？（细节）

相关研究：

 

论文中提到的解决方案是什么，关键点在哪儿？



与3不同的的地方

- 更改backbone 和neck

- 修改了网络的优化策略
  - 消除网格灵敏度 （提出缩放策略）
  - 数据增强
  - Iou threshold（iou阈值） 更改了选取正样本的标准（v3是选iou值最高，v4是选大于iou阈值的所有为正样本）
  - CIOU 新的IOU标准
  - optimizered anchors （优化anchors）







 

![image-20230512095709587](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230512095709587.png)





 CSPDarknet53结构的优势

![image-20230512095808839](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230512095808839.png)



backbone结构

stage1

![image-20230512100246929](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230512100246929.png)

stage2

![image-20230512095834080](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230512095834080.png)

后面的stage和stage2一样





![image-20230512100547049](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230512100547049.png)



a右与b组合起来是PAN

![image-20230512100738838](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230512100738838.png)





![image-20230512101729280](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230512101729280.png)







![image-20230512103212904](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230512103212904.png)





- CSPDarknet53 backbone

- SPP additional module （三个通道增强感受野）
- PANet path-aggregation neck 
- YOLOv3 (anchor based) head 作为 YOLOv4 的架构



![image-20230519094123470](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230519094123470.png)





[网络详解](https://blog.csdn.net/weixin_41560402/article/details/106119774)



