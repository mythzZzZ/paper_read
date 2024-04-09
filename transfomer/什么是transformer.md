

## transformer大体结构

![image-20230307091817512](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307091817512.png)



## transformer细分结构

- 由n个decoder n个encoder组成（图中6个）

- 6个encoder、6个decoder 结构上完全相同 参数不同
- 每个encoder（decoder）分开训练
- encoder与decoder不同
- 后期每个encoder（decoder）共享某些层的参数



![image-20230307092006924](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307092006924.png)



## 单个encoder



![image-20230307092754892](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307092754892.png)

### 输入部分

1. Embedding

   ![image-20230307093113390](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307093113390.png)

nlp基础知识，把我爱你每个字切分，每个字分成512维度的字向量

![image-20230307093532697](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307093532697.png)

普通RNN网络与transformer处理一句话的区别

| RNN                                                      | transformer                                     |
| -------------------------------------------------------- | ----------------------------------------------- |
| 一个个单词传进去处理（先处理我 把我的信息传给爱 处理爱） | 多头注意力机制（并行化） 一次传所有单词一起处理 |
| 序列化                                                   | 忽略了序列化（单词顺序）                        |
| 速度慢                                                   | 速度快                                          |



2.位置嵌入 （embedding 编码加上了位置编码）



​		获取单词位置编码

![image-20230307094253488](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307094253488.png)

把 ==爱== 划分成512维度的位置编码公式 有两条

- 偶数维度用公式1 
- 奇数维度用公式2
- 512维度每个位置对应一个位置编码



transformer的输入

![image-20230307094929422](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307094929422.png)

transformer的输入 = Embedding512 + 位置编码512

（512个位置对应相加）



为什么位置嵌入有用？

![image-20230307095255108](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307095255108.png)

1.使用 sin cos 得到的是绝对位置信息



### 注意力机制

1.  基本的注意力机制

![image-20230307100009542](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307100009542.png)

注意力计算公式
$$
Attention(Q,K,V)=softmax(\frac{QK^T}{\sqrt{d_k}})V
$$
Q,K,V 三个矩阵 softmax归一化得到相似度的向量

Q:Query K:key V:value

![image-20230307101335949](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307101335949.png)

 q  对应婴儿的某种向量

k，v对应不同位置（上下左右）的某种向量

| Q K^T^                              | 得到结果越大 说明婴儿与哪个位置最靠近（最关注）              |
| ----------------------------------- | ------------------------------------------------------------ |
| 设置分别为                          | 0.7 0.1 0.1 0.1 （Q与左上K^T^点乘结果最大 最靠近左上（最关注左上）） |
| $softmax(\frac{QK^T}{\sqrt{d_k}})V$ | 得到的是加权和                                               |







2. 在TRM中怎么操作

获取公式的Q K V矩阵

![image-20230307103410376](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307103410376.png)



![image-20230307103546164](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307103546164.png)

![image-20230307104327187](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307104327187.png)

- softmax归一化 得到的结果相加为 1
- 在softmax中 ==Q K^T^很大 softmax得到的值会很小== 容易梯度消失     $\sqrt{d_k}$ = 8 保持方差控制为1

![image-20230307103643150](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307103643150.png)

- w取多个值 多个 attention



### 残差与LayNorm

==残差结构==

![image-20230307104824642](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307104824642.png)

![image-20230307104932916](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307104932916.png)

X经过函数F(X) (weight layer) 两层得到的结果为F(X) 

输出的结果为F(X)+X （F(X)+X组合起来）这种输入叫残差 

- 残差结构$\oplus$ (缓解梯度消失)

  ![image-20230307111629649](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307111629649.png)



==LayNorm==：Layer Normalization 层归一化







### 前馈神经网络

![image-20230307113132190](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307113132190.png)

Feed Forward 全连接

 add & Normalize 残差和归一化 



## decoder

![image-20230307113723325](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307113723325.png)

mask：把当前时刻的单词之后的所有单词mask掉

让后面的单词不影响前面的预测结果

![image-20230307114059643](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307114059643.png)



encoder与decoder 如何连接起来 

![image-20230307114314157](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307114314157.png)

encoder与每一个decoder做交互





![image-20230307114418285](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307114418285.png)

encoder生产k v矩阵 与decoder 生成的 q矩阵相互交互



![image-20230307114528636](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230307114528636.png)

![image-20230312170413963](C:/Users/Administrator/AppData/Roaming/Typora/typora-user-images/image-20230312170413963.png)