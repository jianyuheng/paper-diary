[论文](https://arxiv.org/abs/1804.07573)
[代码]()

mobilefacenet其实是[mobilenet_v2](https://github.com/jyhengcoder/paper-diary/new/master/papers/mobilenet_v2.md)的改进版本。

## 改进
- 替换全局平均池化层

    虽然中心点的感知域和边角点的感知域是一样的，但是中心点的感知域包括了完整的图片，边角点的感知域却只有部分的图片，因此每个点的权重应该不一样，但是平均池化层却把他们当作一样的权重去考虑了，因此网络表现会下降。
    
作者在此处使用了可分离卷积代替平均池化层，即使用一个7x7x512（512表示输入特征图通道数目）的可分离卷积层代替了全局平均池化，这样可以让网络自己不同点的学习权重。 

此处的可分离卷积层使用的英文名是global depthwise convolution，global表示全局，depthwise表示逐深度，即逐通道的卷积，其实就是之前描述的那种可分离卷积的方式：使用7x7x512的卷积核代替7x7x512x512的卷积核。 
其实这里我们可以发现，后者其实是全卷积


- 采用Insightface的损失函数进行训练。
 
- 一些小细节：通道扩张倍数变小；使用Prelu代替relu;使用batch Normalization。 

## 网络结构
![image](https://github.com/jyhengcoder/paper-diary/new/master/images/mobilefacenet.jpeg)

