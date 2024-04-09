#### Scalablevit: Rethinking the context-oriented generalization of vision transformer



==其他transformer的缺点==

- 基础的自注意力本质上依赖于在预定义的固定维度上运算 ，这限制了它获得有上下文线索和全局表征的泛化能力



==本文提出可扩展的transformer==

它提出一种==可伸缩的自注意力机制SSA==来解除QKV与输入维度的绑定，和一种==基于交互窗口的自注意力IWSA==来实现非重叠窗口的交互，取得优于SOTA性能。



文章提出可缩放自注意力SSA，在空间和通道维度同步引入两个缩放系数（r~n~,r~c~）。SSA在query，key，value矩阵（Q,K,V）中选择性地应用这个两个系数，确保维度更加灵活，不再绑定输入

==把空间维N和通道维C放缩到N⋅r~n~,C⋅r~c~==



提出基于窗口的交互自注意力IWSA，包含一个常规的WSA和一个位置交互模块LIM。通过重新合并独立的value块、聚合相邻窗口的空间信息来建立不重叠区域的交互。





![image-20230322082134074](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230322082134074.png)



==ISWA==

![image-20230322083559328](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20230322083559328.png)

swintransformer 缺少了小块之间的自注意力 

iswa 加上了块间的自注意力