#30daysoftechreading

Day 2/30

Quote of the day: The beginning is the most important part of the work.

Today I chose to read Deep Learning Review by Yann LeCun, Yoshua Bengio & Geoffrey Hinton

Link: https://www.cs.toronto.edu/~hinton/absps/NatureDeepReview.pdf 

This review paper beautifully explains the limitations of conventional machine learning methods to process natural data in their raw form and how representation learning (Deep Learning methods) covers those limitations by allowing a machine to be fed with raw data and to automatically discover the representations needed for detection or classification. 

Deep-learning methods are representation-learning methods with multiple levels of representation, obtained by composing simple but non-linear modules that each transform the representation at one level (starting with the raw input) into a representation at a higher, slightly more abstract level. With the composition of enough such transformations, very complex functions can be learned.

Supervised Learning

This most common form of machine learning wherein we trained the models with labeled examples. We compute an objective function that measures the error (or distance) between the output scores and the desired pattern of scores. The machine then modifies its internal adjustable parameters to reduce this error. These adjustable parameters, often called weights, are real numbers that can be seen as ‘knobs’ that define the input–output function of the machine. 

How does learning happen in Deep Learning systems?

In a typical deep-learning system, there may be hundreds of millions of these adjustable weights, and hundreds of millions of labelled examples with which to train the machine. The learning algorithm computes a gradient vector that, for each weight, indicates by what amount the error would increase or decrease if the weight were increased by a tiny amount. The weight vector is then adjusted in the opposite direction to the gradient vector. The negative gradient vector indicates the direction of steepest descent in objective function, taking it closer to a minimum, where the output error is low on average.

Gradient descent in simple terms: Gradient Descent is an optimization algorithm used for minimizing the cost function in various machine learning algorithms.

Now this gradient descent procedure could be of 3 types:

Batch Gradient Descent: we calculate the gradient on the whole dataset to perform just one update, batch gradient descent can be very slow and is intractable for datasets that don’t fit in memory. Not suitable for large datasets.

Stochastic Gradient Descent: This is a type of gradient descent which processes 1 training example per iteration. Hence this is quite faster than batch gradient descent. But again, when the number of training examples is large, even then it processes only one example which can be additional overhead for the system as the number of iterations will be quite large.

Mini-batch Gradient Descent: This one processed small batches of training examples. In this b examples where b<m are processed per iteration. So even if the number of training examples is large, it is processed in batches of b training examples in one go. Thus, it works for larger training examples and that too with lesser number of iterations.

In practice, most practitioners use a procedure called stochastic gradient descent (SGD)

Many of the current practical applications of machine learning use linear classifiers. A two-class linear classifier computes a weighted sum of the feature vector components. If the weighted sum is above a threshold, the input is classified as belonging to a particular category. But problems such as image and speech recognition require the input–output function to be insensitive to irrelevant variations of the input. This is why shallow classifiers require a good feature extractor that solves the selectivity–invariance dilemma. Though one can use generic non-linear features, as with kernel methods, generalizations with generic features such as those arising with the Gaussian kernel is not very good from the training examples. 

This could be solved with Deep-learning. A deep-learning architecture is a multilayer stack of simple modules, all (or most) of which are subject to learning, and many of which compute non-linear input–output mappings. Each module in the stack transforms its input to increase both the selectivity and the invariance of the representation.

How are these deep learning architectures trained?

The answer to this question is Backpropagation. The backpropagation procedure to compute the gradient of an objective function with respect to the weights of a multilayer stack of modules.The key insight is that the derivative (or gradient) of the objective with respect to the input of a module can be computed by working backwards from the gradient with respect to the output of that module to all the way to the external input.

Many applications of deep learning use feedforward neural network architectures, which learn to map a fixed-size input to a fixed-size output. To go from one layer to the next, a set of units compute a weighted sum of their inputs from the previous layer and pass the result through a non-linear function.

These non-linear functions could be of many types but the most popular non-linear function is the rectified linear unit (ReLU), which is simply the half-wave rectifier f(z)= max(z, 0). The ReLU typically learns much faster in networks with many layers, allowing training of a deep supervised network without unsupervised pre-training.

In the late 1990s, It was widely thought that learning useful, multistage, feature extractors with little prior knowledge was infeasible. But in 2006, the researchers introduced unsupervised learning procedures that could create layers of feature detectors without requiring labelled data. Once the ‘pre-training’ approach was widely accepted and applied, it turned out that the unsupervised pre-training stage was only needed for small data sets. 

There was, however, one particular type of deep, feedforward network that was much easier to train and generalized much better than networks with full connectivity between adjacent layers. These were Convolutional Neural Networks.

Convolutional Neural Networks (ConvNets)

ConvNets are designed to process data that come in the form of multiple arrays, for example a colour image composed of three 2D arrays containing pixel intensities in the three colour channels. Many data modalities are in the form of multiple arrays: 1D for signals and sequences, including language; 2D for images or audio spectrograms; and 3D for video or volumetric images. There are four key ideas behind ConvNets that take advantage of the properties of natural signals: local connections, shared weights, pooling and the use of many layers. 

The architecture of a typical ConvNet (Fig. 2) is structured as a series of stages. The first few stages are composed of two types of layers: convolutional layers and pooling layers.
Units in a convolutional layer are organized in feature maps, within which each unit is connected to local patches in the feature maps of the previous layer through a set of weights called a filter bank. The result of this local weighted sum is then passed through a non-linearity such as a ReLU. All units in a feature map share the same filter bank. Different feature maps in a layer use different filter banks. Although the role of the convolutional layer is to detect local conjunctions of features from the previous layer, the role of the pooling layer is to merge semantically similar features into one. Because the relative positions of the features forming a motif can vary somewhat, reliably detecting the motif can be done by coarse-graining the position of each feature. A typical pooling unit computes the maximum of a local patch of units in one feature map (or in a few feature maps). Neighbouring pooling units take input from patches that are shifted by more than one row or column, thereby reducing the dimension of the representation and creating an invariance to small shifts and distortions. Two or three stages of convolution, non-linearity and pooling are stacked, followed by more convolutional and fully-connected layers. Back propagating gradients through a ConvNet is as simple as through a regular deep network, allowing all the weights in all the filter banks to be trained. 

Deep neural networks exploit the property that many natural signals are compositional hierarchies, in which higher-level features are obtained by composing lower-level ones. In images, local combinations of edges form motifs, motifs assemble into parts, and parts form objects. Similar hierarchies exist in speech and text from sounds to phones, phonemes, syllables, words and sentences. The pooling allows representations to vary very little when elements in the previous layer vary in position and appearance. 

Recent ConvNet architectures have 10 to 20 layers of ReLUs, hundreds of millions of weights, and billions of connections between units.

Distributed Representations

Distributed representations store information as encoded vectors and encoding spreads the information across the entire dimension of the vector, meaning every bit will have some fragment of the stored information. Neural Nets, when trained to predict the next word in a news story, for example, the learned word vectors for Tuesday and Wednesday are very similar, as are the word vectors for Sweden and Norway. Such representations are called distributed representations because their elements (the features) are not mutually exclusive and their many configurations correspond to the variations seen in the observed data. These word vectors are composed of learned features that were not determined ahead of time by experts, but automatically discovered by the neural network. 

It is in opposition to the traditional N-grams approach(counting frequencies of occurrences of short symbol sequences of length up to N). N-grams treat each word as an atomic unit, so they cannot generalize across semantically related sequences of words, whereas neural language models can because they associate each word with a vector of real valued features, and semantically related words end up close to each other in that vector space.

Recurrent Neural-Networks

For tasks that involve sequential inputs, such as speech and language, it is often better to use RNNs. RNNs process an input sequence one element at a time, maintaining in their hidden units a ‘state vector’ that implicitly contains information about the history of all the past elements of the sequence. RNNs are very powerful dynamic systems, but training them has proved to be problematic because the back propagated gradients either grow or shrink at each time step resulting in vanishing and exploding gradients.

Very simple and easy to understand explanation of RNNs:

https://www.youtube.com/watch?v=UNmqTiOnRfg 

There are a lot of applications of RNN such as translations, image caption generation but it suffers in storing long-term dependencies. To handle that, LSTM (Long-short term memory) networks came into picture that use special hidden units, the natural behaviour of which is to remember inputs for a long time.

Working of LSTM:

https://www.youtube.com/watch?v=5dMXyiWddYs 

https://www.youtube.com/watch?v=oOIqrp0h5ig 

LSTM networks have subsequently proved to be more effective than conventional RNNs. 
We expect much of the future progress in vision to come from systems that are trained end-to-end and combine ConvNets with RNNs that use reinforcement learning to decide where to look. Natural language understanding is another area in which deep learning is poised to make a large impact over the next few years. 

Hope you liked the easy explanation of the review paper. Stay tuned for the coming days of #30daysoftechreading
