[www.paperswithcode.com](查模型网站)



Vision transformer



用transformer做图片

  难点：

图片输入序列太长

解决

- 用特征图(图片弄成 )



![image-20230308100508263](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230308100508263.png)

图片弄成图片块 把块当作单词输入到网络



残差网络有归纳编制 vision transformer没有归纳编制

- 没有归纳编制用大数据集的时候效果较好

归纳编制：提前做好的假设（先验信息）

卷积神经网络归纳编制：

- locality 图片相邻的位置有一样的特征
- translation equivariance（平移同变性）
  - $f(g(x)) = g(f(x))$
  - 对图片先做平移后卷积 和先卷积后平移得到的结果一样



生成类模型 判别类模型

判别类模型 成功了更高