# #30daysoftechreading

Day - 7/30

**Quote of the Day** - Be stubborn about your goals and flexible about your methods

Today I chose to watch a really nice video on **"Architectural Elements Of Neural Networks"**. This video really dives deep into the architecture of **Convolutional Neural Networks** and explains the components and the mathematics behind the working of Convolutional Neural Network for a Classification task.

Link: (https://www.youtube.com/watch?v=f9GT9sYP9gk&feature=youtu.be)
### What is a Neural Network?
In simple terms neural network is an attempt to simulate the network of neurons that make up a human brain so that the computer will be able to learn things and make decisions in a humanlike manner.

In technical terms, a neural network is a function that maps an image to a probability distribution over a known set of classes/categories. The prediction for a given image is a given class with the highest probability.

### What is a Convolutional Neural Network?

CNN is a type of neural network model which allows us to extract higher representations for the image content. Unlike the classical image recognition where you define the image features yourself, CNN takes the image’s raw pixel data, trains the model, then extracts the features automatically for better classification.

### Convolutional??

In mathematics (in particular, functional analysis), convolution is a mathematical operation on two functions (f and g) that produces a third function that expresses how the shape of one is modified by the other. The term convolution refers to both the result function and to the process of computing it. It is defined as the integral of the product of the two functions after one is reversed and shifted. And the integral is evaluated for all values of shift, producing the convolution function.
Some features of convolution are similar to cross-correlation: for real-valued functions, of a continuous or discrete variable, it differs from cross-correlation only in that either f(x) or g(x) is reflected about the y-axis; thus it is a cross-correlation of f(x) and g(−x), or f(−x) and g(x). For complex-valued functions, the cross-correlation operator is the adjoint of the convolution operator.
Convolution has applications that include probability, statistics, acoustics, spectroscopy, signal processing and image processing, engineering, physics, computer vision and differential equations.
 
The video breaks into the minute details of a CNN and explains everything in extremely detailed form. It explains the linear components in a Neural Network which are fully connected, convolution and linear up sampling/downsampling and Nonlinear components consists of Activation function, Batch normalization, Max pooling, Softmax function.
 
It covers how the convolution operation happens for the images and what size of output we get with the number of parameters. It compares why convolutional NN are better than fully connected NN for images as the are cheaper to compute and easier to optimize and follow equivariance to translation.
 
**What is Equivariance to translation?** 
 
Features of the images on the top left corner should be treated the same as the same in bottom right corner.
 
It then explained the different types of activation functions and why and where each of them could be used. It also explains batch normalization along with its mathematics.
 
**What is Batch Normalization?**
 
Batch normalization is a technique for training very deep neural networks that standardizes the inputs to a layer for each mini-batch. This has the effect of stabilizing the learning process and dramatically reducing the number of training epochs required to train deep networks.
 
Do watch the video till the end to make sure you have the fondational idea about the working of CNNs.


