**#30daysoftechreading**

**Day-3/30**

**Quote of the day**: Don’t stop when you are tired, stop when you are done.

Today’s pick for the read is another Deep Learning paper **‘UNDERSTANDING DEEP LEARNING REQUIRES RETHINKING GENERALIZATION’**

This paper is ideally suitable for the type of audience who is well aware of the terminologies of Deep Learning. This paper, with extensive systematic experiments, shows how traditional approaches fail to explain why large neural networks generalize well in practice and exhibit remarkably small generalization error, i.e., difference between “training error” and “test error”. 

At the same time, it is certainly easy to come up with natural model architectures that generalize poorly. What is it then that distinguishes neural networks that generalize well from those that don’t? To answer such a question, statistical learning theory has proposed a number of different complexity measures that are capable of controlling generalization error. These include VC dimension (Vapnik, 1998), Rademacher complexity (Bartlett & Mendelson, 2003), and uniform stability (Mukherjee et al., 2002; Bousquet & Elisseeff, 2002; Poggio et al., 2004). Moreover, when the number of parameters is large, theory suggests that some form of regularization is needed to ensure small generalization error. Regularization may also be implicit as is the case with early stopping.

Some experiments to find out how deep learning architecture generalizes when conditioned:

**1. Randomization tests**: When the deep neural networks several standard architectures trained on a copy of the data where the true labels were replaced by random labels, It gave zero training error i.e. it fit the random dta very well.

The test error, of course, is no better than random chance as there is no correlation between the training labels and the test labels. In other words, by randomizing labels alone we can force the generalization error of a model to jump up considerably without changing the model, its size, hyperparameters, or the optimizer.

**Observations**:

1. Neural Networks memorize well.
2. Training time doesn’t increase much. Good optimization on even random labels.
3. Learning properties and processes remain unchanged.

Even if we add random noise i.e. in case of images randomizing the pixels, training error comes to be zero. We observe a steady deterioration of the generalization error as we increase the noise level.

**2. The role of explicit regularization:**

**Regularization** : Regularization is a set of techniques that can prevent overfitting in neural networks and thus improve the accuracy of a Deep Learning model when facing completely new data from the problem domain.

Adding explicit forms of regularization, such as weight decay, dropout, and data augmentation, do not adequately explain the generalization error of neural networks. 

**Weight decay**: When training neural networks, after each update, the weights are multiplied by a factor slightly less than 1. This prevents the weights from growing too large, and can be seen as gradient descent on a quadratic regularization term.

**Dropout**:Dropout is a regularization method that approximates training a large number of neural networks with different architectures in parallel.
During training, some number of layer outputs are randomly ignored or “dropped out.” This has the effect of making the layer look-like and be treated-like a layer with a different number of nodes and connectivity to the prior layer. This helps in preventing overfitting.

**Data Augmentation**: Data augmentation in data analysis are techniques used to increase the amount of data by adding slightly modified copies of already existing data or newly created synthetic data from existing data. It acts as a regularizer and helps reduce overfitting when training a machine learning model.

**Observations**: It may improve generalization performance, but it is not sufficient for controlling generalization error.It appears to be more of a tuning parameter that often helps improve the final test error of a model, but the absence of all regularization does not necessarily imply poor generalization error. As reported by Krizhevsky et al. (2012), l2 regularization  (weight decay) sometimes even helps optimization.

**3. Finite sample expressivity**: In function space, the result shows that even depth-2 networks of linear size can already represent any labeling of the training data. 

**4. The role of implicit regularization** :

Unlike explicit regulation even Stochastic Gradient Descent and Gaussian kernel methods act as an implicit regularizer with small generalization error. Though it could be that some architectures generalize better than other architectures, which needs to be researched more.

While fitting random labels, there’s no need to change the learning rate schedule, it converges quickly, it converges to (over)fit the training set perfectly. Also note that “random pixels” and “Gaussian” start converging faster than “random labels”.

**Early stopping**: During training, the model is evaluated on a holdout validation dataset after each epoch. If the performance of the model on the validation dataset starts to degrade (e.g. loss begins to increase or accuracy begins to decrease), then the training process is stopped. The model at the time that training is stopped is then used and is known to have good generalization performance.This procedure is called “early stopping” and is perhaps one of the oldest and most widely used forms of neural network regularization.

**Observations**: It confirms that early stopping could potentially improve the generalization performance.

**Batch Normalization** : Batch normalization (also known as batch norm) is a method used to make artificial neural networks faster and more stable through normalization of the input layer by re-centering and re-scaling.
Observations: Batch normalization is usually found to improve the generalization performance

In summary, observations on both explicit and implicit regularizers are consistently suggesting that regularizers, when properly tuned, could help to improve the generalization performance. However, it is unlikely that the regularizers are the fundamental reason for generalization, as the networks continue to perform well after all the regularizers are removed. 

The paper further discusses the results of the experiments and concludes that experiments conducted emphasize that the effective capacity of several successful neural network architectures is large enough to shatter the training data. Consequently, these models are in principle rich enough to memorize the training data. This situation poses a conceptual challenge to statistical learning theory as traditional measures of model complexity struggle to explain the generalization ability of large artificial neural networks. Another insight resulting from the experiments is that optimization continues to be empirically easy even if the resulting model does not generalize. This shows that the reasons for why optimization is empirically easy must be different from the true cause of generalization. 
