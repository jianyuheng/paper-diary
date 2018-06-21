[论文](https://arxiv.org/abs/1704.04861)
[代码](https://github.com/Zehaos/MobileNet)

# 网络结构
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/mobilenet_v1.png)

核心思想就是卷积核的巧妙分解，可以有效减少网络参数.

MobileNets模型基于深度可分解的卷积，它可以将标准卷积分解成一个深度卷积和一个点卷积（1 × 1卷积核）。深度卷积将每个卷积核应用到每一个通道，而1 × 1卷积用来组合通道卷积的输出。

