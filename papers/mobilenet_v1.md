[论文](https://arxiv.org/abs/1704.04861)
[代码](https://github.com/Zehaos/MobileNet)

# 网络结构
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/mobilenet_v1.png)

# 深度可分解卷积
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/mobilenet_conv.png)


核心思想就是卷积核的巧妙分解，可以有效减少网络参数.

MobileNets模型基于深度可分解的卷积，它可以将标准卷积分解成一个深度卷积和一个点卷积（1 × 1卷积核）。深度卷积将每个卷积核应用到每一个通道，而1 × 1卷积用来组合通道卷积的输出。

MobileNets使用了大量的3 × 3的卷积核，极大地减少了计算量（1/8到1/9之间），同时准确率下降的很少，相比其他的方法确有优势。

# 模型引入了两个超参数
## width multiplier 宽度乘数
为了构建更小和更少计算量的网络，作者引入了宽度乘数α，作用是改变输入输出通道数，减少特征图数量，让网络变瘦。在α参数作用下，MobileNets某一层的计算量为：
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/width%20multiplier.png)

α常用的配置为1,0.75,0.5,0.25；当α等于1时就是标准的MobileNet。通过参数α可以非常有效的将计算量和参数数量约减到α的平方倍。

## 分辨率因子 resolution multiplier
分辨率因子β的取值范围在(0,1]之间，是作用于每一个模块输入尺寸的约减因子，简单来说就是将输入数据以及由此在每一个模块产生的特征图都变小了，结合宽度因子α，deep-wise结合1x1方式的卷积核计算量为：
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/resolution%20multiplier.png)

