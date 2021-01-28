**#30daysoftechreading**

Day - 4/30

**Quote of the days** - It's a slow process, but quiting won't speed it up.

After 2 days of rigorous research paper reading, I chose to read something lighter today. Today’s pick for the read is an article on  “Understanding PyTorch with an example: a step-by-step tutorial”

Link: (https://towardsdatascience.com/understanding-pytorch-with-an-example-a-step-by-step-tutorial-81fc5f8c4e8e)  

For those who don’t know about Pytorch, PyTorch is an open source machine learning library based on the Torch library, used for applications such as computer vision and natural language processing, primarily developed by Facebook's AI Research lab. PyTorch is also very pythonic, meaning, it feels more natural to use it if you already are a Python developer.

This article will guide you through the main reasons why PyTorch makes it much easier and more intuitive to build a Deep Learning model in Python — autograd, dynamic computation graph, model classes and more — and it will also show you how to avoid some common pitfalls and errors along the way.

**Let’s start understanding what Regression is?**

It is a supervised ML algorithm, in which we have the knowledge of the target label. Any equation, that is a function of the dependent variables and a set of weights is called a regression function.

y ~ f (x ; w) where “Y” is the dependent variable (in the above example, temperature), “X” are the independent variables (humidity, pressure etc) and “b” are the weights of the equation (co-efficients of x terms) and e is the gaussian noise.

**Y = a + bX + e**

For example, the equation can be

y = 0.3 + 2.5 x 2 + 0.6

where 2.5 is the weight and ), 0.3 is the bias and 0.6 is the gaussian noise in this equation. These weights are to be learned by studying the relationship between the dependent and independent variables. 

**So What is learning here means?**

It means the regression Algorithm will try to find the values of the weights and bias such that the predicted output is as near as possible to the original out. This is the training process of the model.

Training is a process where we calculate the gradient descent which minimizes the loss function i.e. the difference between the predicted and true label. You can refer to the mathematics of the training in the article under gradient descent section.

To my amusement, Numpy and Pytorch training has the same structure with slight variations.

**Linear Regression in Numpy**

It’s time to implement our linear regression model using gradient descent using Numpy.

Even though this is a Pytorch tutorial, implementing Numpy firstly introduces the structure of our task, which will remain largely the same and, second, to show you the main pain points so you can fully appreciate how much PyTorch makes your life easier :-)

*For training a model, there are two initialization steps:*

1. Random initialization of parameters/weights (we have only two, a and b) ;
2. Initialization of hyper-parameters (in our case, only learning rate and number of epochs);

Make sure to always initialize your random seed to ensure reproducibility of your results. As usual, the random seed is 42, the least random of all random seeds one could possibly choose.

So I google why 42 is the least random out of curiosity and you can find the story here (https://medium.com/@leticia.b/the-story-of-seed-42-874953452b94)

*For each epoch, there are four training steps:*

1. Compute model’s predictions — this is the forward pass
2. Compute the loss, using predictions and and labels and the appropriate loss function for the task at hand 
3. Compute the gradients for every parameter 
4. Update the parameters

Just keep in mind that, if you don’t use batch gradient descent (our example does),you’ll have to write an inner loop to perform the four training steps for either each individual point (stochastic) or n points (mini-batch).


**Time to move to PYTORCH**

In Deep Learning, we see tensors everywhere. Well, Google’s framework is called TensorFlow for a reason! What is a tensor, anyway?

In Numpy, you may have an array that has three dimensions, right? That is, technically speaking, a tensor.
A scalar (a single number) has zero dimensions, a vector has one dimension, a matrix has two dimensions and a tensor has three or more dimensions. That’s it!

**1. Loading Data, Devices and CUDA**

”How do we go from Numpy’s arrays to PyTorch’s tensors”, you ask? That’s what from_numpy is good for. It returns a CPU tensor, though.

“But I want to use my fancy GPU”, you say. No worries, that’s what to() is good for. It sends your tensor to whatever device you specify, including your GPU (referred to as cuda or cuda:0).

you can use cuda.is_available() to find out if you have a GPU at your disposal and set your device accordingly.

*Refer the code for implementation*

We can also go the other way around, turning tensors back into Numpy arrays, using numpy(). But first Use Tensor.cpu() to copy the tensor to host memory first.

**2. Creating Parameters**

What distinguishes a tensor used for data — like the ones we’ve just created — from a tensor used as a (trainable) parameter/weight?
The latter tensors require the computation of its gradients, so we can update their values (the parameters’ values, that is). That’s what the requires_grad=True argument is good for. It tells PyTorch we want it to compute gradients for us.

Although the last approach worked fine, it is much better to assign tensors to a device at the moment of their creation.

*Refer the code for implementation*

Note - In PyTorch, every method that ends with an underscore (_) makes changes in-place, meaning, they will modify the underlying variable.

**3. Autograd**

Now that we know how to create tensors that require gradients, let’s see how PyTorch handles them

Autograd is PyTorch’s automatic differentiation package. Thanks to it, we don’t need to worry about partial derivatives, chain rule or anything like it.

Do you remember the starting point for computing the gradients? It was the loss, as we computed its partial derivatives w.r.t. our parameters. Hence, we need to invoke the backward() method from the corresponding Python variable, like, loss.backward().

If you check the method’s documentation, it clearly states that gradients are accumulated. So, every time we use the gradients to update the parameters, we need to zero the gradients afterwards. And that’s what zero_() is good for.

*Refer the code for implementation*

torch.no_grad()  allows us to perform regular Python operations on tensors, independent of PyTorch’s computation graph.

**4. Optimizer**

An optimizer takes the parameters we want to update, the learning rate we want to use (and possibly many other hyper-parameters as well!) and performs the updates through its step() method.

Besides, we also don’t need to zero the gradients one by one anymore. We just invoke the optimizer’s zero_grad() method and that’s it!

*Refer the code for implementation*

**5. Loss**

We now tackle the loss computation. As expected, PyTorch got us covered once again. There are many loss functions to choose from, depending on the task at hand. Since ours is a regression, we are using the Mean Square Error (MSE) loss.

Notice that nn.MSELoss actually creates a loss function for us — it is NOT the loss function itself. Moreover, you can specify a reduction method to be applied, that is, how do you want to aggregate the results for individual points — you can average them (reduction=’mean’) or simply sum them up (reduction=’sum’).

**6. Model**

In PyTorch, a model is represented by a regular Python class that inherits from the Module class.

*The most fundamental methods it needs to implement are:*

__init__(self): it defines the parts that make up the model —in our case, two parameters, a and b.

forward(self, x): it performs the actual computation, that is, it outputs a prediction, given the input x.

In the __init__ method, we define our two parameters, a and b, using the Parameter() class, to tell PyTorch these tensors should be considered parameters of the model they are an attribute of.

Why should we care about that? By doing so, we can use our model’s parameters() method to retrieve an iterator over all model’s parameters, even those parameters of nested models, that we can use to feed our optimizer (instead of building a list of parameters ourselves!).
Moreover, we can get the current values for all parameters using our model’s state_dict() method.

*Training Step*
So far, we’ve defined an optimizer, a loss function and a model. Scroll up a bit and take a quick look at the code inside the loop. Would it change if we were using a different optimizer, or loss, or even model? If not, how can we make it more generic?

Well, I guess we could say all these lines of code perform a training step, given those three elements (optimizer, loss and model),the features and the labels.

So, how about writing a function that takes those three elements and returns another function that performs a training step, taking a set of features and labels as arguments and returning the corresponding loss?

Then we can use this general-purpose function to build a train_step() function to be called inside our training loop.

**7. Dataset**

In PyTorch, a dataset is represented by a regular Python class that inherits from the Dataset class. You can think of it as a kind of a Python list of tuples, each tuple corresponding to one point (features, label).

*The most fundamental methods it needs to implement are:*

__init__(self) : it takes whatever arguments needed to build a list of tuples — it may be the name of a CSV file that will be loaded and processed; it may be two tensors, one for features, another one for labels; or anything else, depending on the task at hand.

There is no need to load the whole dataset in the constructor method (__init__). If your dataset is big (tens of thousands of image files, for instance), loading it at once would not be memory efficient. It is recommended to load them on demand (whenever __get_item__ is called).

__get_item__(self, index): it allows the dataset to be indexed, so it can work like a list (dataset[i]) — it must return a tuple (features, label) corresponding to the requested data point. We can either return the corresponding slices of our pre-loaded dataset or tensors or, as mentioned above, load them on demand (like in this example).

__len__(self): it should simply return the size of the whole dataset so, whenever it is sampled, its indexing is limited to the actual size.

*Refer the code for implementation*

**8. DataLoader**

Until now, we have used the whole training data at every training step. It has been batch gradient descent all along. This is fine for our ridiculously small dataset, sure, but if we want to go serious about all this, we must use mini-batch gradient descent. Thus, we need mini-batches. Thus, we need to slice our dataset accordingly.

So we use PyTorch’s DataLoader class for this job. We tell it which dataset to use (the one we just built in the previous section), the desired mini-batch size and if we’d like to shuffle it or not. That’s it!

Our loader will behave like an iterator, so we can loop over it and fetch a different mini-batch every time.

*Refer the code for implementation*

**9. Evaluation**

This is the last part of our journey — we need to change the training loop to include the evaluation of our model, that is, computing the validation loss. The first step is to include another inner loop to handle the mini-batches that come from the validation loader , sending them to the same device as our model. Next, we make predictions using our model (line 23) and compute the corresponding loss (line 24).

*That’s pretty much it, but there are two small, yet important, things to consider:*

torch.no_grad(): even though it won’t make a difference in our simple model, it is a good practice to wrap the validation inner loop with this context manager to disable any gradient calculation that you may inadvertently trigger — gradients belong in training, not in validation steps;

eval(): the only thing it does is setting the model to evaluation mode (just like its train() counterpart did), so the model can adjust its behavior regarding some operations, like Dropout.

*Refer the code for implementation*


