VISION PERMUTATOR: A PERMUTABLE MLP-LIKE ARCHITECTURE FOR VISUAL RECOGNITION



基于MLP提出提出新的视觉分类网络 vision permutator

基本架构

![image-20230412151836238](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230412151836238.png)



- Channel-MLP是transformer的FFN结构

vision permutator

- 提出新的结构Permute-MLP layer
- ![image-20230412151903012](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230412151903012.png)

- 对 H W C 空间都进行编码
- Input Tokens 是三维的输入信息(h w c patch Embedding后得到的)



![image-20230413110146880](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230413110146880.png)

空间信息编码的方法先按通道分组(segment_dim(分组数) = input的 H = input W)

对H进行信息编码：

- 每一组把H放到C的位置然后堆叠起来做全连接（全连接相等于空间信息编码）

同理w也只这样
