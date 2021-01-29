#30daysoftechreading

Day - 5/30

Quote of the Day : 

As students, we all develop ML models and make predictions from it. The question is, are those models deployed on a service or scalable for thousands of user traffic? If not we are just half way through. Keeping these in mind I chose to read an article on “Scaling Machine Learning from 0 to millions of users — part 1”

Link: https://towardsdatascience.com/scaling-machine-learning-from-0-to-millions-of-users-part-1-a2d36a5e849 

This article gives really great suggestions of do’s and don’ts to create a scalable ML model.

It assumes we start the journey at the stage where you’ve trained a model on your local machine (or a local dev server), using a popular open source library like scikit-learn, TensorFlow or Apache MXNet. Maybe you’ve even implemented your own algorithm. You’ve measured the model’s accuracy using your test set, and things look good. Now you’d like to deploy the model to production in order to check its actual behaviour, run A/B tests, etc. Where to start?

Batch prediction or real-time prediction?

First, you should figure out whether your application requires batch prediction (i.e. collect a large number of data points, process them periodically and store results somewhere), or real-time prediction (i.e. send a data point to a web service and receive an immediate prediction ). The reason why it brings this point early on is because it has a large impact on deployment complexity.

Real-time prediction sounds more appealing, but it also comes with stronger requirements, inherent in web services: high availability, the ability to handle traffic bursts, etc. Batch is more relaxed, as it only needs to run every now and then.

If you have a deadline or have a customer demo in a few days, and you need to harden the existing solution since you do not have time to feature a new ML service called Amazon SageMaker. Use the Deep Learning AMI.

It is maintained by AWS, this Amazon Machine Image comes pre-installed with a lot of tools and libraries that you’ll probably need: open source, NVIDIA drivers, etc. Not having to manage them will save you a lot of time, and will also guarantee that your multiple instances run with the same setup.

The AMI also comes with the Conda dependency and environment manager, which lets you quickly and easily create many isolated environments: that’s a great way to test your code with different Python versions or different libraries, without unexpectedly clobbering everything.
Last but not least, this AMI is free of charge, and just like any other AMI, you can customize if you really have to.

The article also advises the following steps:


breaking the code into different sections

Your application code and your prediction code have different requirements. Unless you have a compelling reason to do so, they shouldn’t live under the same roof.

Let’s look at some reasons why:

Deployment: do you want to restart or update your app every time you update the model? Or ping your app to reload it or whatever? No no no no. Keep it simple: when it comes to decoupling, nothing beats building separate services.

Performance: what if your application code runs best on memory-intensive instances and your ML model requires a GPU? How will you handle that trade-off? Why would you favour one or the other? Separating them lets you pick the best instance type for each use case.

Scalability: what if your application code and your model have different scalability profiles? It would be a shame to scale out on GPU instances because a small piece of your application code is running hot. Again, it’s better to keep things separated, this will help take the most appropriate scaling decisions as well as reduce cost.

It also says that model-independent actions (formatting, logging, etc.) should stay in the application, whereas model-dependent actions (feature engineering) should stay close to the model to avoid deployment inconsistencies.

Build a prediction service

Separating the prediction code from the application code doesn’t have to be painful, and you can reuse solid, scalable tools to build a prediction service. 

You can use Scikit-learn, Tensorflow, Apache MXNet


Containerize your application

Since you’ve decided to split your code, it recommends that you use the opportunity to package the different pieces in Docker containers: one for training, one for prediction, one (or more) for the application. It’s not strictly necessary at this stage.

Containers make it easy to move code across different environments (dev, test, prod, etc.) and instances. They solve all kinds of dependency issues, which tend to pop up even if you’re only managing a small number of instances. Later on, containers will also be a pre-requisite for larger-scale solutions such as Docker clusters or Amazon SageMaker.

The benefits of doing the above steps:

The Deep Learning AMI provides a stable, well-maintained foundation to build on.

Containers help you move and deploy your application with much less infrastructure drama than before.

Prediction now lives outside of your application, making testing, deployment and scaling simpler.

      4. If you can use them, model servers save you most of the trouble of writing a prediction service.

There is another article in continuation to this one which would be covered in 
Day-6. Stay tuned :)
