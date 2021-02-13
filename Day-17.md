#30daysoftechreading

Day 17/30

Quote of the day: You never fail, until you stop trying!!

I came across a question today, Is a 1 * 1 convolution operation the same as scaling the input by a single scalar constant? While searching the answer for this I came accross the article "A Gentle Introduction to 1×1 Convolutions to Manage Model Complexity". 

Link: (https://machinelearningmastery.com/introduction-to-1x1-convolutions-to-reduce-the-complexity-of-convolutional-neural-networks/)

In this article, you will discover how to use 1×1 filters to control the number of feature maps in a convolutional neural network.

Pooling can be used to down sample the content of feature maps, reducing their width and height whilst maintaining their salient features.

A problem with deep convolutional neural networks is that the number of feature maps often increases with the depth of the network. This problem can result in a dramatic increase in the number of parameters and computation required when larger filter sizes are used, such as 5×5 and 7×7.

To address this problem, a 1×1 convolutional layer can be used that offers a channel-wise pooling, often called feature map pooling or a projection layer. This simple technique can be used for dimensionality reduction, decreasing the number of feature maps whilst retaining their salient features. It can also be used directly to create a one-to-one projection of the feature maps to pool features across channels or to increase the number of feature maps, such as after traditional pooling layers.

Benefits of 1*1 Convolution:

1. The 1×1 filter can be used to create a linear projection of a stack of feature maps.
2. The projection created by a 1×1 can act like channel-wise pooling and be used for dimensionality reduction.
3. The projection created by a 1×1 can also be used directly or be used to increase the number of feature maps in a model.

The article gives a nice explaination about:

- Convolutions Over Channels
- Problem of Too Many Feature Maps
- Downsample Feature Maps With 1×1 Filters
- Examples of How to Use 1×1 Convolutions
- Examples of 1×1 Filters in CNN Model Architectures
