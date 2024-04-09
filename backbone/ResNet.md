

==ResNet 残差网络==



解决网络越深性能变差的问题




$$
F(x) = H(x) - x
$$

$$
F(x) + x
$$





如何解决残差连接输入输出不一样的问题

- 使用1x1的卷积 改变维度





![image-20230321104500626](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230321104500626.png)

- 左右两图效果一样
- 残差 -- 残差  一样