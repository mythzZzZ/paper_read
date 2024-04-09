sw :shift window



问题：

图像resolution

图片patch：每一个块

MLP

layer norm 



池化操作：增大卷积核的感受野  提取多尺寸特征





检测和分割任务多尺寸特征最重要

常见目标检测多尺寸特征的方法（FPN）

FPN：a feature pyramid network

![image-20230310202856854](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230310202856854.png)

当有一个分层式的卷积神经网络之后，每一个卷积层出来的特征它的receptive field（感受野）不一样，能抓住不同尺寸的物体的特征，很好处理这个物体不同尺寸的问题



常见分割处理多尺寸特征的方法（unet）

![image-20230310203151055](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230310203151055.png)

提出一个skip connection的方法





---

# swin transformer的特点？

- win自注意力
- swin自注意力
- patch merging







## swin

有移动窗口的transformer

移动窗口的作用：

- 处理输入的数据
- swin（移动窗口）的作用减少序列长度
- 自注意力在移动窗口（小窗口）上做
  - vit在整个图上做自注意力
- 往右下角移动窗口（让窗口之间有联系 可以自注意力）

![image-20230310204321706](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230310204321706.png)

1.左边 块内自注意力 块与块之间不能交互自注意力

![image-20230310204819734](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230310204819734.png)

2.大窗口往右下移动 然后在划分小块 此时新的小块与原来的小块组成不一样 这样小块做自注意力 可以全局就可以建立联系





移动窗口 然后在割补块 （==循环位移==）

小窗口不同颜色之间不能做自注意力

- 加入掩码的方式计算不同颜色块的自注意力
- 最后把块还原

![image-20230311110935475](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230311110935475.png)













==移动窗口的自注意力==

| 全局自注意力 | 窗口自注意力 |
| ------------ | ------------ |
| 平方倍复杂度 | n倍复杂度    |
|              |              |

![image-20230311101608140](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230311101608140.png)

自注意力机制复杂度的计算


$$
\Omega(MSA) = 4h\omega C^2+2(h\omega )^2C
$$

$$
\Omega(W-MSA) = 4h\omega C^2 + 2M^2h\omega C
$$


公式一： hw为窗口大小

​	正方形 -> qkv

- hw x C 的矩阵 乘以一个 c x c的矩阵得到 qkv 
  - 此时复杂度为 hw X C^2^ 
    - qkv各有一个 复杂度 所有得到 3hwC^2^
- q 和K乘 ， A和v乘分别得到一个复杂度 (hw)^2^c 复杂度
  - 加起来为 2(hw)^2^c
- 最后一个proj(hw x C  乘以 c x c)
  - 得到复杂度 hwC^2^
- 最后得到公式1的复杂度



公式2：



​	每个窗口大小变成 mxm 此时==每个窗口自注意力==公式为
$$
4m^2C^2+2m^4C
$$


一共有 $\frac{h}{m} ✖\frac{w}{m}$个窗口 乘以每个窗口的自注意力得到公式2











---



## path merging

==这个过程相当于卷积神经网络的池化==

相邻patch 合成大patch （小patch合成大patch 感受野增大了 ==抓住多尺寸特征信息==）



下采样特征图的效果

下采样两倍：每隔一个点选一个

![image-20230311095827388](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230311095827388.png)

- 图上的值是序号

- 图1经过采样（图里相同的序号）得到图2四个张量 四个张量拼接成图三

- 用空间的维度换取更多的通道（类似于池化）

- 图3经过卷积操作得到图4（ 降维）



![image-20230311100459796](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230311100459796.png)

得到特征图之后 用了一个global averge polling（全局池化）

把特征拉直为1传进去