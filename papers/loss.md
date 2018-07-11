## softmax loss

[交叉熵](https://blog.csdn.net/tsyccnh/article/details/79163834)

[损失函数求导](https://blog.csdn.net/zb1165048017/article/details/64122890) 

[冗余参数集](http://ufldl.stanford.edu/wiki/index.php/Softmax回归)

## triplet loss

[原理以及梯度推导](https://blog.csdn.net/tangwei2014/article/details/46788025)


## face loss
[center loss](https://blog.csdn.net/u014230646/article/details/53764079)
- softmax loss的缺点是它只会使得类间特征分离，并不会使属于同一类的特征积聚。这样的特征对于人脸识别来说不够有效。

[SphereFace/A-Sotfmax loss](https://www.cnblogs.com/heguanyou/p/7503025.html)
- 使得类间距离的最小值大于类内距离的最大值,同时保留较大的裕量;
- 归一化softmax前的全连接层权重,则优化的是角度. 
提出了一种角度的softmax.学习到角度判别性的特征。可以看成在一个超球面的流形上施加判别性的约束。先验假设是：人脸是位于流形上的。通过参数m定量调整角度的裕量，并导出了m的下界。证明易懂。

[CosFace/AM-Softmax loss](https://blog.csdn.net/u014230646/article/details/79487404)
- 这篇是对sphereface的改进之一，具体的方法是把角度裕量从cos(mθ)改进为cos(θ)+m
，主要的好处是这样改进之后容易收敛。相当于原始余弦函数在y轴上的偏移，使得分类更加困难。

[ArcFace loss](https://blog.csdn.net/u014230646/article/details/79487720)
- 相当于原始的余弦函数在x轴上向左偏移。这样做了之后，在角度值为180°的时候分类难度基本不变，而角度值较小的时候分类更加困难。相当于在角度值较小的时候加了裕量。




