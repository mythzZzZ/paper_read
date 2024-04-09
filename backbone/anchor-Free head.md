# FCOS

- sub-box区域内为正样本
- 一个GT范围内不是正样本就是负样本
- 若有标签重复分配问题，把该anchor分配给面积最小的GT





# SimOTA 

（YOLOX）

- 计算COS

- 根据cos选最小k个

- 选取最小k个点里，这些点在fixed center area（sub-box）里面的点为正样本 （k为超参）

- 正样本选取个数为k个IOU值相加得到取整

- 一个GT内不是正样本其余的点为负样本

  



# ATSS

1、计算每个 gt bbox 和多尺度输出层的所有 anchor 之间的 IoU
2、计算每个 gt bbox 中心坐标和多尺度输出层的所有 anchor 中心坐标的 l2 距离
3、遍历每个输出层，遍历每个 gt bbox，找出当前层中 topk (超参，默认是 9 )个最小 l2 距离的 anchor 。假设一共有 l 个输出层，那么对于任何一个 gt bbox，都会挑选出 topk×l 个候选位置
4、对于每个 gt bbox，计算所有候选位置 IoU 的均值和标准差，两者相加得到该 gt bbox 的自适应阈值
5、遍历每个 gt bbox，选择出候选位置中 IoU 大于阈值的位置，该位置认为是正样本，负责预测该 gt bbox





# TOOD(T-head)

 1. 计算所有 bbox与 gt 之间的对齐度
 2. 选择 top-k bbox 作为每个 gt 的候选项
 3. 将正样品的中心限制在 gt 内(因为Anchor-Free检测器只能预测大于0的距离)
 4. 如果一个Anchor被分配给多个gt，将选择IoU最高的那个。
  
