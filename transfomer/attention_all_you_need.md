==attention is all you need==



encode:输入词 生成词向量

decode:一个词一个词的解码



multi-head attention:

layer-norm: 把每一个feature（向量）变成均值为0方差为1

- 在每个小batch里算layer-norm

- 均值
- 方差

![image-20230319094706553](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230319094706553.png)



![image-20230319095530707](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230319095530707.png)



masked multi-head attention:让multi-head在t时刻的输出看不到t时刻之后的输入(因为attention可以看到全局的输入)



qkv:

![image-20230319100754780](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230319100754780.png)

k-v是一开始给定的向量



当有一个q(query)过来，求这个q的v值

- 这个q的v由三个v相加得来 每个v的权重不一样
- 权重根据q与k的相似度计算得到
- 







假设一个句子长度为n 则他的输入是要 n个长为d的向量

输入经过encode然后输出的维度一样

![image-20230319104248547](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230319104248547.png)



- 每一个向量对应一个输出向量

  ![image-20230319104429751](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230319104429751.png)

  一个输出是每个输入的加权和

   如果是多头注意力则输出有一点不一样



![image-20230319104719448](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230319104719448.png)

masked的作用 求t时刻的输出时 t时刻后的输入权重为0