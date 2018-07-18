 Binarized Neural Networks: Training Neural Networks with Weights and Activations Constrained to +1 or−1的工作是基于
- BinaryConnect: Training Deep Neural Networks with binary weights during propagations
- NEURAL NETWORKS WITH FEW MULTIPLICATIONS
这两篇文章的。

 **二值网络是将权值W和隐藏层激活值二值化1或者-1。**
 
 
 通过二值化，使模型的参数占用更小的存储空间；同时利用位移操作来代替网络中的乘法运算，大大降低了运算时间。
 由于二值网络只是将网络的参数和激活值二值化，并没有改变网络的结构。因此我们主要关注如何二值化，以及二值化后参数如何更新。
 同时关注一下如何利用二进制位操作实现GPU加速计算的。
 
 ## 二值化
 
 - Deterministic（确定性方法）
大于0就为+1，小于0则为-1。

- Stochastic方法
对x计算一个概率p，当p大于一个阙值（计算机随机产生）时为+1，否则为-1。

由于Stochastic方法需要由硬件生成随机数，这比较难实施。所以论文中的实验用的是Deterministic方法。

## 训练时的前向传播
二值网络训练时的权值参数W，必须包含实数型的参数，然后将实数型权值参数二值化得到二值型权值参数，然后利用二值化后的参数计算得到实数型的中间向量，该向量再通过Batch Normalization操作，得到实数型的隐藏层激活向量。如果不是输出层的话，就将该向量二值化。

除了输出层，其他隐藏层都经过二值化。所以在求Batch Normalization的参数时，必须先求二值操作层（我们把二值化也当做一层来看待）的梯度。

 
