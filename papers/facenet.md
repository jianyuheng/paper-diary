[速览](https://blog.csdn.net/stdcoutzyx/article/details/46687471)
[代码](https://github.com/davidsandberg/facenet)

## 网络要点
通过去掉softmax层的卷积神经网络提取特征，经过L2归一化得到新的特征表示，基于这个特征表示计算triplet loss。
