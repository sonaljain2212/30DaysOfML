#30daysoftechreading

Day 19/30

Quote of the day:

Happy Monday!!

I have been reading a lot about neural networks and thus it was necessary for me to get familiar with so many important optimization techniques that are there in NN. So I chose to read "An overview of gradient descent optimization algorithms" article.

link: (https://ruder.io/optimizing-gradient-descent/index.html#adam)


Before we dive in lets get the basics used:

- Exponentially weighted averages:

To understand exponentially weighted average, we need to first understand moving averages, weighted averages and then we can easily understand exponentially weighted average:

  - Moving averages:

We can easily relate this with stock price and it is widely used in this domain. A moving average is calculated from the average closing prices for a specified period.  A moving average typically uses daily closing prices, but it can also be calculated for other timeframes. Other price data such as the opening price or the median price can also be used. At the end of the new price period, that data is added to the calculation while the oldest price data in the series is eliminated.

  - Weighted moving average:

Weighted moving averages assign a heavier weighting to more current data points since they are more relevant than data points in the distant past. The sum of the weighting should add up to 1 (or 100 percent). In the case of the simple moving average, the weightings are equally distributed

Exponential moving averages (EMAs) are also weighted toward the most recent prices, but the rate of decrease between one price and its preceding price is not consistent. The difference in the decrease is exponential. Rather than every preceding weight being 1.0 smaller than the weight in front of it, there might be a difference between the first two period weights of 1.0, a difference of 1.2 for the two periods after those periods, and so on.



Momentum:

The method of momentum is designed to accelerate learning, especially in the face of high curvature, small but consistent gradients, or noisy gradients. The momentum algorithm accumulates an exponentially decaying moving average of past gradients and continues to move in their direction. Momentum aims primarily to solve two problems: poor conditioning of the Hessian matrix and variance in the stochastic gradient. Formally, the momentum algorithm introduces a variable v that plays the role of velocity—it is the direction and speed at which the parameters move through parameter space. The velocity is set to an exponentially decaying average of the negative gradient.

![alt text](https://ruder.io/content/images/2015/12/without_momentum.gif)

![alt text](https://ruder.io/content/images/2015/12/with_momentum.gif)

Previously, the size of the step was simply the norm of the gradient multiplied by the learning rate. Now, the size of the step depends on how large and how aligned a sequence of gradients are. The step size is largest when many successive gradients point in exactly the same direction. If the momentum algorithm always observes gradient g, then it will accelerate in the direction of −g, until reaching a terminal velocity where the size of each step is ||g||/1 − α.  This explains the basic form of the momentum update, but what speciﬁcally are the forces? One force is proportional to the negative gradient of the cost function: −∇θ J(θ). This force pushes the particle downhill along the cost function surface. The gradient descent algorithm would simply take a single step based on each gradient, but the Newtonian scenario used by the momentum algorithm instead
uses this force to alter the velocity of the particle. We can think of the particle as being like a hockey puck sliding down an icy surface. Whenever it descends a steep part of the surface, it gathers speed and continues sliding in that directionuntil it begins to go uphill again. One other force is necessary. If the only force is the gradient of the cost function, then the particle might never come to rest. Imagine a hockey puck sliding down one side of a valley and straight up the other side, oscillating back and forth forever,assuming the ice is perfectly frictionless. To resolve this problem, we add one other force, proportional to −v(t). In physics terminology, this force corresponds to viscous drag, as if the particle must push through a resistant medium such as syrup. This causes the particle to gradually lose energy over time and eventually converge to a local minimum. 
Why do we use
−v(t) and viscous drag in particular? Part of the reason to use −v(t) is mathematical convenience—an integer power of the velocity is easy to work with. Yet other physical systems have other kinds of drag based on other integer powers of the velocity. For example, a particle traveling through the air
experiences turbulent drag, with force proportional to the square of the velocity,
while a particle moving along the ground experiences dry friction, with a force
of constant magnitude. We can reject each of these options. Turbulent drag,
proportional to the square of the velocity, becomes very weak when the velocity is
small. It is not powerful enough to force the particle to come to rest. A particle
with a nonzero initial velocity that experiences only the force of turbulent drag.
 
AdaGrad:

The AdaGrad Algorithm individually adapts the learning
rates of all model parameters by scaling them inversely proportional to the square
root of the sum of all the historical squared values of the gradient (Duchi et al.,
2011). The parameters with the largest partial derivative of the loss have a
correspondingly rapid decrease in their learning rate, while parameters with small
partial derivatives have a relatively small decrease in their learning rate. The net
eﬀect is greater progress in the more gently sloped directions of parameter space.
In the context of convex optimization, the AdaGrad algorithm enjoys some
desirable theoretical properties. Empirically, however, for training deep neural
network models, the accumulation of squared gradients from the beginning of
training can result in a premature and excessive decrease in the eﬀective learning
rate. AdaGrad performs well for some but not all deep learning models.

 
RMSProp:

The RMSProp Algorithm modiﬁes AdaGrad to perform better in
the nonconvex setting by changing the gradient accumulation into an exponentially
weighted moving average. AdaGrad is designed to converge rapidly when applied to
a convex function. When applied to a nonconvex function to train a neural network,
the learning trajectory may pass through many diﬀerent structures and eventually
arrive at a region that is a locally convex bowl. AdaGrad shrinks the learning rate
according to the entire history of the squared gradient and may have made the
learning rate too small before arriving at such a convex structure. RMSProp uses
an exponentially decaying average to discard history from the extreme past so that
it can converge rapidly after ﬁnding a convex bowl, as if it were an instance of the
AdaGrad algorithm initialized within that bowl.
 
Adam:
 
The name “Adam” derives from
the phrase “adaptive moments.” In the context of the earlier algorithms, it is
perhaps best seen as a variant on the combination of RMSProp and momentum
with a few important distinctions. First, in Adam, momentum is incorporated
directly as an estimate of the ﬁrst-order moment (with exponential weighting) of
the gradient. The most straightforward way to add momentum to RMSProp is to
apply momentum to the rescaled gradients. The use of momentum in combination
with rescaling does not have a clear theoretical motivation. Second, Adam includes
bias corrections to the estimates of both the ﬁrst-order moments (the momentum
term) and the (uncentered) second-order moments to account for their initialization
at the origin (see algorithm 8.7). RMSProp also incorporates an estimate of the (uncentered) second-order moment; however, it lacks the correction factor. Thus,
unlike in Adam, the RMSProp second-order moment estimate may have high bias
early in training. Adam is generally regarded as being fairly robust to the choice
of hyperparameters, though the learning rate sometimes needs to be changed from
the suggested default.
 
 
 
 
 
 
 
 
 
 
