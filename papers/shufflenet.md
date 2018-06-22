[论文](https://arxiv.org/pdf/1707.01083.pdf)
[代码](https://arxiv.org/pdf/1707.01083.pdf)
# 创新
## 推广群卷积(group convolution)
### 群卷积
我们假设上一层的输出feature map有N个，即通道数channel=N，也就是说上一层有N个卷积核。再假设群卷积的群数目M。那么该群卷积层的操作就是，先将channel分成M份。每一个group对应N/M个channel，与之独立连接。然后各个group卷积完成后将输出叠在一起（concatenate），作为这一层的输出channel。
然而如果多个组卷积堆叠在一起，会有一个副作用： 某个通道输出仅从一小部分输入通道中导出，如下图(a)所示，这样的属性降低了通道组之间的信息流通，降低了信息表示能力。

其造成的问题是，输出通道只和输入的某些通道有关，导致全局信息流通不畅，网络表达能力不足。
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/shuffle_1.png)
 - 图a是之前的一种ResNet网络结构模块，其参考了“MobileNet”的实现。其中的DWConv指的是 depthwise convolution。
 - 图b是本文给出的一种模块(输出前后feature的size不变)， 相比于图a,只是将第一个1x1卷积改成了group convolution，同时后续增加通道 shuffle。
 - 图c是本文给出的另一种模块(输出前后feature的size变小，但通道数增加)，主要是为了应对下采样问题。 注意，最后的合并操作由原来的 “Add” 变成了 “Concat”, 目的是为了增加通道数。
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/shuffle_2.png)

## 深度可分卷积(depthwise separable convolution)
参照mobilenet

## shuffle unit
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/shuffle_unit.png)
给定一个计算限制，ShuffleNet可以使用更宽的特征映射。我们发现这对小型网络很重要，因为小型网络没有足够的通道传递信息。
需要注意的是:虽然深度卷积可以减少计算量和参数量，但在低功耗设备上，与密集的操作相比，计算/存储访问的效率更差。故在ShuffleNet上我们只在bottleneck上使用深度卷积，尽可能的减少开销.


# 网络结构
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/shufflenet.png)
主要分为三个阶段：

- 每个阶段的第一个block的步长为2，下一阶段的通道翻倍
- 每个阶段内的除步长其他超参数保持不变
- 每个ShuffleNet unit的bottleneck通道数为输出的1/4(和ResNet设置一致)
这里主要是给出一个baseline。在ShuffleNet Unit中，参数g控制逐点卷积的连接稀疏性(即分组数)，对于给定的限制下，越大的g会有越多的输出通道，这帮助我们编码信息。

定制模型需要满足指定的预算，我们可以简单的使用放缩因子s控制通道数，ShuffleNets×即表示通道数放缩到s倍。




