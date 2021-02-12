# #30daysoftechreading

Day 16/30

Quote of the day: It's okay to take a break and start againg with a full blow!!

The quote above because I took a break yesterday and I believe it is needed sometimes. So I am now in the 2nd half of my 30 day journey and I can't tell you how good it feels!! So today I chose to learn somthing interesting about how the parameters are calulated in a Convolution Neuural Network. I came across this article "Understanding and Calculating the number of Parameters in Convolution Neural Networks (CNNs)" for learning the calculations.

Link: (https://towardsdatascience.com/understanding-and-calculating-the-number-of-parameters-in-convolution-neural-networks-cnns-fc88790d530d)

Different layers in a CNN:

- Input layer: Input layer has nothing to learn, at it’s core, what it does is just provide the input image’s shape. So no learnable parameters here. Thus number of parameters = 0.

- CONV layer: This is where CNN learns, so certainly we’ll have weight matrices. To calculate the learnable parameters here, all we have to do is just multiply the by the shape of width m, height n, previous layer’s filters d and account for all such filters k in the current layer. Don’t forget the bias term for each of the filter. Number of parameters in a CONV layer would be : ((m * n * d)+1)* k), added 1 because of the bias term for each filter. The same expression can be written as follows: ((shape of width of the filter * shape of height of the filter * number of filters in the previous layer+1)*number of filters). Where the term “filter” refer to the number of filters in the current layer.
- POOL layer: This has got no learnable parameters because all it does is calculate a specific number, no backprop learning involved! Thus number of parameters = 0.
- Fully Connected Layer (FC): This certainly has learnable parameters, matter of fact, in comparison to the other layers, this category of layers has the highest number of parameters, why? because, every neuron is connected to every other neuron! So, how to calculate the number of parameters here? You probably know, it is the product of the number of neurons in the current layer c and the number of neurons on the previous layer p and as always, do not forget the bias term. Thus number of parameters here are: ((current layer neurons c * previous layer neurons p)+1*c).

