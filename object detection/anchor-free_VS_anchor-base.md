yolov3[yolov3](https://blog.csdn.net/qq_37541097/article/details/81214953?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522169953590516800185893266%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=169953590516800185893266&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-1-81214953-null-null.nonecase&utm_term=yolo&spm=1018.2226.3001.4450)

![image-20231109211948361](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20231109211948361.png)

- 预测四个位置信息因子
- tx ty 经过simg激活加Cx Cy才得到相对于特征图原点的坐标
- tw，th是相对于anchor-base的anchor的缩放因子，经过相对于anchor的计算公式得到预测边框的宽度和高度



yolox[yolox](https://blog.csdn.net/qq_37541097/article/details/125132817?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522169953558716800222880515%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=169953558716800222880515&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-1-125132817-null-null.nonecase&utm_term=yolox&spm=1018.2226.3001.4450)

![image-20231109212159937](https://zhangwenkang666.oss-cn-beijing.aliyuncs.com/image-20231109212159937.png)

- tx,ty是直接相对于当前特征图gridcell左上角的偏移量
- tw,th不是相对于anchor的宽高因子

