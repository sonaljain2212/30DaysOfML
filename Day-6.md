# 30daysoftechreading

Day - 6/30

**Quote of the day**: Keep Going. Today you are a step closer than you were yesterday.

Already 20% through...yayy!!! Let’s continue yesterday's article on “**Scaling Machine Learning from 0 to millions of users**” — part 2. 

Link: (https://medium.com/faun/scaling-machine-learning-from-0-to-millions-of-users-part-2-80b0d1d7fc61)

In real life scenarios there could be situations like traffic soon starting to increase, data piles up, more models need to be trained, technical and business stakes are getting higher, and let’s face it, the current architecture will go underwater soon. Thus this article focuses on scaling training to a large number of machines.

## Will scaling up fix it?

Yes - it can be a short-term solution to use a large server for training and prediction. Amazon EC2 has a ton of instance types to pick from, and all it takes is stopping your instance, changing the instance type, and starting it again.

No - because it’s only a temporary solution. It’s fine to use bigger instances, until there is no bigger instance. Then what? It’s also quite possible that your workload won’t scale nicely, and won’t make full use of the additional hardware (RAM, CPU cores, I/O, etc.). A marginal performance gain isn’t worth the extra spend. Most of all, scaling up will simply delay the inevitable. Keep doing it, and the only thing you’ll end up with is a bigger problem to solve.

## Scaling out

When it comes to training Machine Learning (ML) models, the top requirements are actually pretty simple:
1. Reliable, scalable storage for your data sets. 
2. Elastic compute clusters, that can be started on-demand in lots of different configurations (hardware, frameworks, etc.).
3. As little ops as possible: ML is what you should focus on, because ML is what turns your raw data into revenue / profit / improver customer experience.

## Storage

Keeping it straight, your data goes to Amazon S3. You now get up to 25 Gigabit per second between EC2 and S3.

## Compute Options


The article gives a very good comparison of using Amazon EC2, Amazon EMR, Container services, Amazon SageMaker based on the requirements.

### 1. Amazon EC2

The Deep Learning AMI makes your life much simpler. It’s packed with open source tools and libraries optimized by AWS. Horovod, a popular library for distributed training, is also included. All of this will make it much easier to set up efficient, distributed training clusters.

Whichever AMI you use, setting up a training cluster means:
Firing up a bunch of instances,
Picking one as the leader, and setting up distributed training. That usually involves listing hostnames / IP addresses of other machines in the cluster.
Start training,
Once training is complete, grab the trained model and save it in Amazon S3.
Shut the training cluster down.

The main concern for using EC2 here is unless you automate all of this (with AWS CloudFormation, Terraform, CLI scripts, etc.), you will waste a ton of money. So if you have a cluster provisioning script that each developer can run to get their own training cluster. It can be a good enough reason to stick to EC2 for training.

 ### 2. Amazon EMR

Amazon EMR in a ML discussion? Well, yes TensorFlow and Apache MXNet are part of the EMR distribution, and of course, Spark MLlib is also included. EMR supports compute-optimized instances (c5 and p3), so it looks like we have everything we need.

Here are a few good reasons to run training jobs on EMR:

- You already use EMR for other tasks, with solid automation (on-demand clusters,steps, etc.) and cost optimization (spot instances).
- Your data requires a lot of ETL, and Hive / Spark would work great for that. Why not run everything in one place?
- Spark MLlib has the algos you need.
- You read somewhere that there a (SageMaker SDK for Spark), so that could be another option for the future.

And equally good reasons NOT to do it:
- You don’t have time or skills to automate and optimize costs. GPU-based EMR clusters running 24/7 at on-demand price with zero load <rolls a D100 for sanity check… >
- You’re using neither TensorFlow, Apache MXNet nor Spark MLlib. Yes, you could install additional packages to your clusters, but that’s extra work.
- Your ETL and ML jobs have conflicting instance requirements. Let’s say that they would respectively run best on 8 r5.4xlarge and 2 p3.8xlarge for training. How do you compromise? 

That’s a hard call, and you may end up picking an instance type that’s suboptimal for both ETL and training or creating a dedicated GPU cluster.

 ### 3. Container services

This would also pay dividends when deploying to Docker clusters, whether on Amazon ECS or Amazon EKS. You can run any workload in a Docker container, and you can move it around without any restriction, from your laptop to your production environment. When running on AWS, costs can be squeezed with auto scaling, reserved instances, spot instances, etc. From a training perspective, containers give you full flexibility to use any open source library, or even your own custom code. All popular ML/DL libraries provide base images, which you can either run directly or customize, and these will save you a lot of time.

Thanks to auto scaling now supporting (mixed instances types), different instance types can coexist within the same cluster. Thus, you can easily add compute-optimized instances to any cluster and schedule your ML/DL training there. Of course, you can also create a dedicated cluster for training if you think that makes more sense. Last but not least, GPU instances are supported on both services, with GPU-optimized AMIs to boot.

### 4.Amazon SageMaker
One more option to go: Amazon SageMaker. I’ve discussed it at lengths in previous posts and talks (start here for a recent overview), and as the most recent service of the bunch, I’ve saved it for last to see where it improves on previous options with respect to training large jobs.

A quick reminder:

- All activity in SageMaker is driven by a high-level Python SDK.
- Training is based on on-demand, fully-managed instances. Zero infrastructure work. Spot instances are not available.
- Models may be trained using AWS-maintained built-in algorithms and optimized frameworks (same ones as in the Deep Learning AMI), as well as custom algorithms.
- Distributed training is built-in. Zero setup.

At the end, the article and author recommends to still go to SageMaker, because unlike ECS and EKS, SageMaker is built for Machine Learning only given the number of benefits it has but it is also dependent on a lot of factors.




