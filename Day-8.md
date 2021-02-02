# #30daysoftechreading

Day - 8/30

**Quote of the day**:

Today I chose to read a paper “**Visualizing and Understanding Convolutional Networks**”  in the lines of Day 7 video explaining the Convolution Neural Networks.

Large Convolutional Network models have demonstrated impressive classification performance on the ImageNet benchmark. So this paper explains why they perform so well, or how they might be improved. The paper introduces a novel visualization technique that gives insight into the function of intermediate feature layers and the operation of the classier.

The authors performed a study to understand the contribution of model layers and from the results they got to know the ImageNet models generalizes very well for different datasets jand outperforms the current state-of-the-art results on Caltech-101 and Caltech-256 datasets.

This paper introduces a visualization technique that reveals the input stimuli that excite individual feature maps at any layer in the model. It also allows us to observe the evolution of features during training and to diagnose potential problems with the model. The visualization
technique it proposes uses a multi-layered Deconvolutional Network (deconvnet), to project the feature activations back to the input pixel space.

**How it works?**

These models map a color 2D input image xi, via a series of layers, to a probability vector yi over the C different classes. Each layer consists of 

- (i) convolution of the previous layer output (or, in the case of the 1st layer, the input image) with a set of learned filters (filter) ;
- (ii) passing the responses through a rectified linear function (relu(x) = max(x; 0)) (reLu) ; 
- (iii) [optionally] max pooling over local neighborhoods and (Max Pooling )
- (iv) [optionally] a local contrast operation that normalizes the responses
across feature maps.

The top few layers of the network are conventional fully-connected networks and the final layer isa softmax classifier.

We train these models using a large set of N labeled images fx; yg, where label yi is a discrete variable indicating the true class. A cross-entropy loss (cross-entropy loss)  function, suitable for image classification, is used to compare yi hat and yi. The parameters of the network (filters in the convolutional layers, weight matrices in the fully-connected layers and biases) are trained by back propagating the derivative of the loss with respect to the parameters throughout the network, and updating the parameters via stochastic gradient descent.

**Visualization with a Deconvnet**

A deconvnet can be thought of as a convnet model that uses the same components (ltering, pooling) but in reverse, so instead of mapping pixels to features does the opposite. The paper presents a novel way to map these activities back to the input pixel space, showing what input pattern originally caused a given activation in the feature maps using Deconvolutional Neural Network.

To start, an input image is presented to the convnet and features computed throughout the layers. To examine a given convnet activation, we set all other activations in the layer to zero and pass the feature maps as input to the attached deconvnet layer. Then we successively (i) Unpool , (ii) Retify and (iii) Filter  to reconstruct the activity in the layer beneath that gave rise to the chosen activation. This is then repeated until input pixel space is reached.

The paper further shows the features visualization for CovNets and the results of the experiments conducted with some architecture changes. It also shows how the ImageNet trained model can generalize well to other datasets. For Caltech-101 and Caltech-256, the datasets are similar enough that we can beat the best reported results, in the latter case by a significant margin.
 
For a easy understanding of CNN, take a look on “Beginners guide to Convolutional Neural Networks” on 
(https://towardsdatascience.com/a-beginners-guide-to-convolutional-neural-networks-cnns-14649dbddce8) 




