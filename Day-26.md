# #30daysoftechreading

Day 26/30

Quote of the Day: Don't wait for it to happen, make it happen!!

Just 5 more days to go!! Couldn't believe I was able to keep my consistency with a few breaks. Today I chose to read a paper on ResNets titled as "Deep Residual Learning for Image Recognition". This paper presents a residual learning framework to ease the training of networks that are substantially deeper than those used previously. The depth of representations is of central importance for many visual recognition tasks. Using ensemble of these residual nets authors were able to achieves 3.57% error on the ImageNet test set.

### Background
Researchers observed that it makes sense to affirm that “the deeper the better” when it comes to convolutional neural networks. This makes sense, since the models should be more capable (their flexibility to adapt to any space increase because they have a bigger parameter space to explore). However, it has been noticed that after some depth, the performance degrades. This was one of the bottlenecks of VGG. They couldn’t go as deep as wanted, because they started to lose generalization capability.

### Motivation
Since neural networks are good function approximators, they should be able to easily solve the identify function, where the output of a function becomes the input itself.


![alt text](https://miro.medium.com/max/141/1*c2Pdaa_8i-akMdb4sz00qw.png)

Following the same logic, if we bypass the input to the first layer of the model to be the output of the last layer of the model, the network should be able to predict whatever function it was learning before with the input added to it.


![alt text](https://miro.medium.com/max/221/1*Pj5r0fEcNkodaSoa7ESjgw.png)

The intuition is that learning f(x) = 0 has to be easy for the network.

### What problems ResNets solve?

One of the problems ResNets solve is the famous known vanishing gradient. This is because when the network is too deep, the gradients from where the loss function is calculated easily shrink to zero after several applications of the chain rule. This result on the weights never updating its values and therefore, no learning is being performed.
With ResNets, the gradients can flow directly through the skip connections backwards from later layers to initial filters.

### Architecture

Since ResNets can have variable sizes, depending on how big each of the layers of the model are, and how many layers it has, we will follow the described by the authors in the paper [1] — ResNet 34 — in order to explain the structure after these networks. If you have taken a look at the paper, you will have probably seen some figures and tables like the following ones, that you are struggling to follow. Lets depict those figures by going into the detail of every step. In here we can see that the ResNet (the one on the right) consists on one convolution and pooling step (on orange) followed by 4 layers of similar behavior. Each of the layers follow the same pattern. They perform 3x3 convolution with a fixed feature map dimension (F) [64, 128, 256, 512] respectively, bypassing the input every 2 convolutions. Furthermore, the width (W) and height (H) dimensions remain constant during the entire layer. The dotted line is there, precisely because there has been a change in the dimension of the input volume (of course a reduction because of the convolution). Note that this reduction between layers is achieved by an increase on the stride, from 1 to 2, at the first convolution of each layer; instead of by a pooling operation, which we are used to see as down samplers. 

![alt text](https://miro.medium.com/max/625/1*kBlZtheCjJiA3F1e0IurCw.png)

In the table, there is a summary of the output size at every layer and the dimension of the convolutional kernels at every point in the structure.

![alt text](https://miro.medium.com/max/875/1*I2557MCaFdNUm4q9TfvOpw.png)
