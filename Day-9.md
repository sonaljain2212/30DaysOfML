# #30daysoftechreading

Day 9/30

**Quote of the day**: Life is too short to skip a tech read day!! :p

After struggling to find the motivation to read today, I thought of reading a light article on a topic that has been intriguing me lately which is "Convolutional Neural Networks". So I chose to read  “A Beginner’s Guide to Convolutional Neural Networks (CNNs)” for the most basic (yet very important) understanding of this topic!!

Link: https://towardsdatascience.com/a-beginners-guide-to-convolutional-neural-networks-cnns-14649dbddce8  

### What is a Convolution?
A convolution is how the input is modified by a filter. In convolutional networks, multiple filters are taken to slice through the image and map them one by one and learn different portions of an input image. Imagine a small filter sliding left to right across the image from top to bottom and that moving filter is looking for, say, a dark edge. Each time a match is found, it is mapped out onto an output image.

The article very well shows the operation for 2D convolution. Convolution in 3D is just like 2D, except you are doing the 2d work 3 times, because there are 3 color channels.

-Padding: If you want to keep the output image at the same width and height without decreasing the filter size, you can add padding to the original image with zero’s and make a convolution slice through the image.

feature map:An output channel of the convolutions is called a feature map. It encodes the presence or absence, and degree of presence of the feature it detects.

-Translation-Invariant
Another interesting fact is CNNs are somewhat resistant to translation such as an image shifting a bit, which would have a similar activation map as the one before shifting. It’s because the convolution is a feature detector and if it’s detecting a dark edge and the image is moved to the bottom, then dark edges will not be detected until the convolution is moved down.

-Pooling
Note that pooling is a separate step from convolution. Pooling is used to reduce the image size of width and height. Note that the depth is determined by the number of channels. As the name suggests, all it does is it picks the maximum value in a certain size of the window. Although it’s usually applied spatially to reduce the x, y dimensions of an image.

-Max-Pooling
Max pooling is used to reduce the image size by mapping the size of a given window into a single result by taking the maximum value of the elements in the window.

-Average-Pooling
It's the same as max-pooling except that it averages the windows instead of picking the maximum value.

The article further explains the setup of Convolutional Neural Networks and calculations in each layer in a very easy to understand manner. Do read the full article twice to understand how During the training process, the network’s building blocks are repeatedly altered in order for the network to reach optimal performance and to classify images and objects as accurately as possible.
 
