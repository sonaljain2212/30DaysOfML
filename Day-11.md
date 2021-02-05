# #30dayoftechreading

Day - 11/30

**Quote of the Day**: Success of the maximum utilization of ability that you have!!

While Studying ML concepts, you would very often see two terminologies coming which you should definitely know and understand well. They are Maximum Likelihood estimation and Maximum A Posterior, thus I decided to read an article on “Maximum Likelihood Estimation VS Maximum A Posterior”.

Link: https://towardsdatascience.com/mle-vs-map-a989f423ae5c 

Both Maximum Likelihood Estimation (MLE) and Maximum A Posterior (MAP) are used to estimate parameters for a distribution. MLE is also widely used to estimate the parameters for a Machine Learning model, including Naïve Bayes and Logistic regression.


### **Maximum Likelihood Estimation:**

The goal of MLE is to infer Θ in the likelihood function p(X|Θ).

![alt text](https://miro.medium.com/max/294/1*Yn-toKQ53M7jdMMxGBYSbA.gif)

Because of duality, maximize a log likelihood function equals to minimize a negative log likelihood. In Machine Learning, minimizing negative log likelihood is preferred. For example, it is used as a loss function, cross entropy, in the Logistic Regression.

The coin example in the article shows that When the sample size is small, the conclusion of MLE is not reliable.


### **Maximum A Posterior:**

Recall, we could write posterior as a product of likelihood and prior using Bayes’ rule:

![alt text](https://miro.medium.com/max/411/1*HiJ4JaVAc6IIFqQqDW87wg.png)

In the formula, p(y|x) is posterior probability; p(x|y) is likelihood; p(y) is prior probability and p(x) is evidence.

![alt text](https://miro.medium.com/max/430/1*nnB9V9HPHsMdofRyh_UbPw.png)

In order to get MAP, we can replace the likelihood in the MLE with the posterior:

![alt text](https://miro.medium.com/max/430/1*Vp-Wy_o3FIvg_rBnRRGSzg.png)

Comparing the equation of MAP with MLE, we can see that the only difference is that MAP includes prior in the formula, which means that the likelihood is weighted by the prior in MAP.
In the special case when prior follows a uniform distribution, this means that we assign equal weights to all possible value of the Θ. In this case, MAP can be written as:

![alt text](https://miro.medium.com/max/430/1*Vp-Wy_o3FIvg_rBnRRGSzg.png)
