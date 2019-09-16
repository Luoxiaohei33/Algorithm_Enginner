#                                 Mobilenet

https://github.com/tensorflow/models/tree/master/research/slim/nets/mobilenet

## 一  mobilenetV1

### 1  Depthwise separable convolution

​        mobilenetV1核心是将正常的卷积conv分解为可分离卷积depthwise conv和1x1的逐点卷积pointwise conv

 mobilenetV1基本结构：

![img](https://pic3.zhimg.com/80/v2-2fb755fbd24722bcb35f2d0d291cee22_hd.jpg)

​            mobilenetV1网络结构：

![img](https://chenrudan.github.io/blog/2018/04/05/mobilenetv1v2/mobilenet_4.png)

## 二  mobilenetV2

### 1  解决：

```
1）Relu造成的低维度数据坍塌。即channel少的feature map不应后接Relu，否则会破坏feature map.

2）没有复用特征。即神经网络训练中如果某个卷积节点权重值变为0后，由于relu函数，该节点输出都是0，反向梯度也为0，因此不会再变化，从而造成特征退化，而resnet能够解决特征复用问题。
```

mobilenetV2基本结构：

![](https://pic4.zhimg.com/80/v2-11719566eb9051abff065016cffdf27f_hd.jpg)

### 2  主要提出：Linear Bottlenecks + Inverted residual block

```
1) Linear Bottlenecks
   去掉了第二个1x1 point conv的激活函数，换成线性函数。作者认为激活函数在高维空间能够有效的增加非线性，而在低维空间时则会破坏特征，不如线性的效果好。
   
2)  Inverted residual block
   先由1x1 的point wise conv 对feature map进行维度增加，再接Rule6，降低relu对特征的破坏，经3x3 depthwise conv后接1x1 point conv 进行通道降维，之后接linear。
```



## 三  mobilenetV3

不适合移动端部署，放弃吧少年，有钱人的土豪玩的网络。





