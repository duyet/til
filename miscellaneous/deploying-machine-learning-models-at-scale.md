---
description: 'https://algorithmia.com/blog/deploying-machine-learning-at-scale'
---

# Deploying Machine Learning Models at Scale

Deploying machine learning models at scale is one of the most pressing challenges faced by the community of data scientists today, and as ML models get more complex, it’s only getting harder. The most common way machine learning gets deployed today is **on powerpoint slides**.

We estimate that fewer than 5 percent of commercial data science projects make it to production. If you want to be part of that share, you need to understand how deployment works, why machine learning is a unique deployment problem, and how to navigate this messy ecosystem.

---

![](../.gitbook/assets/word-image-9.png)

## Machine learning has a few unique features that makes deploying it at scale harder

Deploying regular software applications is hard—but when that software is a machine learning pipeline, it’s worse.

1. **Multiple Data Science Languages**
   1. **R, Python, Scalar ...**
2. **Data Science Languages Can Be Slow**
3. **Machine Learning Can Be Extremely Compute Heavy, and Relies on GPUs**
4. **Machine Learning Compute Works In Spikes**
   1. Once your algorithms are trained, they’re not used consistently––your customers will only call them when they need them. That can mean that you’re only supporting 100 API calls at 8:00 AM, but 1 Million at 8:30 AM. Scaling up and down like that while making sure not to pay for servers you don’t need is a nightmare.

> After taking months to write out your \(awesome\) models, you’re going to need to hand them over to engineering to deploy at scale. That process can take months, and the models you end up with may not at all resemble what you handed them originally. And if you want to make small changes after, or continually improve your models with new data? Forget about it.



