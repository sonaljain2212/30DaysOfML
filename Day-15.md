# #30daysoftechreading

Day 15/30

**Quote of the Day**: Keep your eyes on the stars and feets on the ground!!

So yesterday I read a paper on Batch Normalization and How batch normalization combats “Internal Covariate shift” while training Deep Neural Nets. Interestingly today the paper I read, titled “**How Does Batch Normalization Help Optimization?**” demonstrates that such distributional stability of layer inputs has little to do with the success of BatchNorm. 

Link: (https://arxiv.org/pdf/1805.11604.pdf)

Instead, the paper uncovered a more fundamental impact of BatchNorm on the training process: it makes the optimization landscape significantly smoother. This smoothness induces a more predictive and stable behavior of the gradients, allowing for faster training.

The paper proposes the experiments wherein the authors train networks with random noise injected after BatchNorm layers. Specifically, they perturb each activation for each sample in the batch using i.i.d. noise sampled from a non-zero mean and non-unit variance distribution. They also emphasize that this noise distribution changes at each time step. Note that such noise injection produces a severe covariate shift that skews activations at every time step. Consequently, every unit in the layer experiences a different distribution of inputs at each time step. They then measure the effect of this deliberately introduced distributional instability on BatchNorm’s performance. They observe that the performance difference between models with BatchNorm layers, and “noisy” Batch-Norm layers is almost non-existent. Also, both these networks perform much better than standard networks. Moreover, the “noisy” BatchNorm network has qualitatively less stable distributions than even the standard, non-BatchNorm network, yet it still performs better in terms of training. 

Moreover, adding the same amount of noise to the activations of the standard (non-BatchNorm) network prevents it from training entirely. Clearly, these findings are hard to reconcile with the claim that the performance gain due to BatchNorm stems from increased stability of layer input distributions.

Surprisingly, they observe that networks with BatchNorm often exhibit an increase in ICS. This is particularly striking in the case of DLN. In fact, in this case, the standard network experiences almost no ICS for the entirety of training, whereas for BatchNorm it appears uncorrelated. We emphasize that this is the case even though BatchNorm networks continue to perform drastically better in terms of attained accuracy and loss. (The stabilization of the BatchNorm VGG network later in training is an artifact of faster convergence.) This evidence suggests that, from an optimization point of view BatchNorm might not even reduce the internal covariate shift.

It parametrizes the underlying optimization problem to make its landscape significantly more smooth. The first manifestation of this impact is improvement in the Lipschitzness of the loss function. That is, the loss changes at a smaller rate and the magnitudes of the gradients are smaller too. There is, however, an even stronger effect at play. Namely, BatchNorm’s reparametrization makes gradients of the loss more Lipschitz too. In other words, the loss exhibits a significantly better “effective” β-smoothness3 . These smoothening effects impact the performance of the training algorithm in a major way. To understand why, recall that in a vanilla (non-BatchNorm), deep neural network, the loss function is not only non-convex but also tends to have a large number of “kinks”, flat regions, and sharp minima. This makes gradient descent–based training algorithms unstable, e.g., due to exploding or vanishing gradients, and thus highly sensitive to the choice of the learning rate and initialization

We observe that all the normalization strategies offer comparable performance to BatchNorm. In fact, for deep linear networks, `1– normalization performs even better than BatchNorm. Note that, qualitatively, the `p–normalization techniques lead to larger distributional shifts than the vanilla, i.e., unnormalized, networks, yet they still yield improved optimization performance. Also, all these techniques result in an improved smoothness of the landscape that is similar to the effect of BatchNorm. This suggests that the positive impact of BatchNorm on training might be somewhat serendipitous. Therefore, it might be valuable to perform a principled exploration of the design space of normalization schemes as it can lead to better performance. 



