# #30daysoftechreading

**Day 18/30**

**Quote of the day**: The best preparation for tomorrow is doing your best today.

Today I chose to read a paper on “ADAM: A METHOD FOR STOCHASTIC OPTIMIZATION”.

This paper introduces adam optimization, an algorithm for first-order gradient-based optimization of stochastic objective functions, based on adaptive estimates of lower-order moments*. The focus of this paper is on the optimization of stochastic objectives with high-dimensional parameters spaces. In these cases, higher-order optimization methods are 
ill-suited, and discussion in this paper will be restricted to first-order methods.

Link: (https://arxiv.org/pdf/1412.6980.pdf)

The Adam method is straightforward to implement, is computationally efficient, has little memory requirements, is invariant to diagonal rescaling of the gradients, and is well suited for problems that are large in terms of data and/or parameters. The method is also appropriate for non-stationary objectives and problems with very noisy and/or sparse gradients. Empirical results demonstrate that Adam works well in practice and compares favorably to other stochastic optimization methods. 

The method computes individual adaptive learning rates for different parameters from estimates of first and second moments of the gradients; the name Adam is derived from adaptive moment estimation.

Our method is designed to combine the advantages of two recently popular methods: AdaGrad (Duchi et al., 2011), which works well with sparse gradients, and RMSProp (Tieleman & Hinton, 2012), which works well in on-line and non-stationary settings. Some of Adam’s advantages are that the magnitudes of parameter updates are invariant to rescaling of the gradient, its stepsizes are approximately bounded by the stepsize hyperparameter, it does not require a stationary objective, it works with sparse gradients**, and it naturally performs a form of step size annealing***.

*the first and second moments, as used in the arithmetic mean (first), and variance (second) are examples of low-order statistics.

**sparse gradient learning (SGL), for variable selection and dimension reduction via learning the gradients of the prediction function directly from samples. By imposing a sparsity constraint on the gradients, variable selection is achieved by selecting variables corresponding to non-zero partial derivatives, and effective dimensions are extracted based on the eigenvectors of the derived sparse empirical gradient covariance matrix.

***Simulated annealing is a technique that is used to find the best solution for either a global minimum or maximum, without having to check every single possible solution that exists.

