[论文](http://arxiv.org/abs/1602.07360 )
[代码](https://github.com/DeepScale/SqueezeNet)

SqueezeNet的核心在于Fire module，Fire module 由两层构成，分别是squeeze层+expand层，如下图所示，squeeze层是一个1*1卷积核的卷积层，expand层是 1*1 和 3*3卷积核的卷积层，expand层中，把 1*1 和 3*3 得到的 feature map 进行 concat。

Fire module输入的feature map为H*W*M的，输出的feature map为H*M*(e1+e3)，可以看到feature map的分辨率是不变的，变的仅是维数，也就是通道数，这一点和VGG的思想一致。


![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/squeezenet.png)
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/squeezenet_1.png)
![image](https://github.com/jyhengcoder/paper-diary/blob/master/images/squeezenet_2.png)


Fire module输入的feature map为H*W*M的，输出的feature map为H*M*(e1+e3)，可以看到feature map的分辨率是不变的，变的仅是维数，也就是通道数，这一点和VGG的思想一致。

首先，H*W*M的feature map经过Squeeze层，得到S1个feature map，这里的S1均是小于M的，以达到“压缩”的目的。

其次，H*W*S1的特征图输入到Expand层，分别经过1*1卷积层和3*3卷积层进行卷积，再将结果进行concat，得到Fire module的输出，为 H*M*(e1+e3)的feature map。

fire模块有三个可调参数：S1，e1，e3，分别代表卷积核的个数，同时也表示对应输出feature map的维数，在本文提出的SqueezeNet结构中，e1=e3=4s1

