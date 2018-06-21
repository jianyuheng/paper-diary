[论文](https://arxiv.org/abs/1801.04381)
[代码](https://github.com/MG2033/MobileNet-V2)

# inverted resnet
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/mobilenet_v2_inverted_resnet.png)
本文实验“扩张”倍数为6。 通常residual block里面是 “压缩”→“卷积提特征”→“扩张”，MobileNetV2就变成了 “扩张”→“卷积提特征”→ “压缩”，因此称为Inverted residuals。

# Linear bottlenecks
压缩后损失了部分特征，避免Relu层损失更多的特征。

# 网络结构
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/mobilenet_v2.png)
其中：t表示“扩张”倍数，c表示输出通道数，n表示重复次数，s表示步长stride。 
先说两点有误之处吧： 
1. 第五行，也就是第7~10个bottleneck，stride=2，分辨率应该从28降低到14；如果不是分辨率出错，那就应该是stride=1； 
2. 文中提到共计采用19个bottleneck，但是这里只有17个。
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/mobilenet_v2_bottleneck.png)

特别的，针对stride=1 和stride=2，在block上有稍微不同，主要是为了与shortcut的维度匹配，因此，stride=2时，不采用shortcut。 具体如下图： 
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/mobilenet_v2_stride_block.png)

可以发现，除了最后的avgpool，整个网络并没有采用pooling进行下采样，而是利用stride=2来下采样。

![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/mobilenet_v2_1.png)

