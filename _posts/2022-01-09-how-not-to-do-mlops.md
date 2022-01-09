---
layout: post
title:  "How (not) to do MLOps"
date:   2022-01-09 22:00:32 +0530
categories: learning mlops mlengineering
---

My company - well, my team - organizes what is called the Paper Reading Club. The idea is for each of us to present a paper to the entire team that we find fascinating and relevant to what we do at work. So for the paper presentation meet that happened a couple of weeks ago, I decided to present [“Using AntiPatterns to avoid MLOps Mistakes”](https://arxiv.org/abs/2107.00079).

Our thoughts have been big on MLOps and ML Engineering since last year. I’m primarily a data scientist but also a part of the MLOps team and I found this paper pretty relevant to what we do.

> "Just as design patterns codify best software engineering practices, ***antipatterns*** provide a vocabulary to describe defective practices and methodologies."

These practices include steps from an entire ML model deployment life cycle, including the post deployment tasks of performance tracking, monitoring, etc. Nine antipatterns are defined. I’ve also added some thoughts from my experiences in building models and deploying them at scale.

> 💡 There’s also this nice podcast on [The Data Exchange]([https://thedataexchange.media/mlops-anti-patterns/](https://thedataexchange.media/mlops-anti-patterns/)) that you can listen to.

## Now to start with these antipatterns...

### Data Leakage

One of the biggest and most common issue we try to avoid is leakage of information in our datasets. Models make use of data/information that it is not supposed to (or not available during inference) and this gives us incorrect results during our evaluation stage. Time series data is also prone to this when the train-test split is not carried out sequentially. For imbalanced data, performing incorrect oversampling is another example  - oversampling before splitting the data into train and test sets. Other examples include the preprocessing stages where standard normalization is performed, again, before the train-test split. 

### Act Now, Reflect Never

Most of the times, the predictions from our models are used directly without any checks, filtering or even inspection. This leads to issues around concept drift and erroneous predictions. 

A good way to avoid these could be to define systems and processes that look into the drift in the data and predictions. Data drift dashboards - simple dashboards that can monitor and track data metrics can really help here, even if it is manual inspection. The predictions can also pass through such dashboard, and simple aggregated metrics and charts can be used to track the distribution of predictions. If you have alerting in place if certain thresholds are violated, you can avoid a lot of debugging.

### Tuning-Under-The-Carpet

While I could not necessarily understand how this can be strict antipattern, I definitely see this a nice-to-have guideline that can save a lot of dollars and time. This has to do with how hyper-parameters are tuned. The authors propose that random search (within a defined range) of the hyper-parameter space yields a computationally cheap and an equivalent alternative to grid search. This can bring a lot of difference to your iterations (cycles) and cost. It is also super important to document everything related to hyper-parameters so that it is reproducible (including the random seed used)

I’ve personally found tools like [Weights and Biases](https://wandb.ai/site) and [Neptune.ai](https://neptune.ai/) to be really helpful here. These tools increase your experimentation cycles multi-fold and that is the most important practice when it comes to applying ML to solve problems in most companies.

### PEST - Perceived Empirical Superiority

Machine learning research is driven by the empirical verification and validation of theoretical proposals. Novel contributions to applied machine learning research comprise (i) validation of previously unverified theoretical proposals, (ii) new theoretical proposals coupled with empirical verification, or (iii) effective augmentations to existing learning pipelines to yield improved empirical performance. The authors mention that often the empirical verification of newly proposed ML methodologies is insufficient, flawed, or found wanting, leading to the definition of the term PEST. They talk about the need for identical experimental pipelines for comparison and evaluation of ML models.

### Bad Credit Assignment

This antipattern talks about the failure to correctly identify the source of performance gains. While your model architecture and those super tuned hyper-parameters will boost your performance, failure to attribute (possible) gains to other tasks like clever problem formulations, certain preprocessing steps, etc. could lead to issues in the future.

Extending the previously mentioned data drift dashboard, and using the experiment tracking tools, one should be able to define inferences from every model deployed be able to appropriately attribute.

### Grade-your-own-exam

These are issues that arise with incorrect evaluation and validation practices. Testing and evaluation data should be sampled independently, and for a robust performance analysis, should be kept hidden until model development is complete and must be used only for final valuation.

One way to tackle to this is by investing in Feature Stores. These can be independent Ground Truth systems, powered by data pipelines that creates your train-test datasets periodically, ensuring that you can always have test sets that are unseen.

### Set and Forget

Many of us adopt this mentality when it comes to model training. This antipattern talks about concept drift and the plausible need to set up model re-training jobs and pipelines. There has been work around Bayesian modelling for detection and adaptation of concept drifts.

The aforementioned inference dashboards can help catch these drifts, simply by manual inspection. This could be automated too, of course.

### Communicate with Ambivalence

Predictions are important, but the uncertainty in the predictions could be more important. For situations where decisive actions are taken based on the model predictions, and if these actions are critical (related to finance, health, etc.) then these uncertainties become crucial. Mechanisms to report uncertainties in predictions becomes important enabling fallback systems and more confident models to kick in if something goes wrong.

### And finally, Data Crisis as a Service

Back to the concept of Feature (data) store. Every pipeline that produces your data should be documented and it’s details communicated. An effective way to do this is by building a data catalog that is in sync with the feature store. This ensures that new pipelines can be easily created and scheduled adhering to the predefined standards of the feature store, and more importantly sets up processes that enable replication of these pipelines whenever required. This also helps to track data lineage.

### Authors’ recommendations

Technical debt is something that has been scaring engineers away since decades. Tech debt for us (read ML folks) isn’t really related to software engineering, but it is everything to do with data pipelines, model pipelines, model (re-)training jobs, feedback mechanism, and so on. 

To tackle them, some of their specific recommendations are:

- Use these antipatterns to set up processes to avoid these mistakes
- Use assertions to track data quality
- Document data lineage and create ‘audit trails’
- Use ensembles and fallback systems to the event of errors
- Ensure human-in-the-loop operational capability at multiple levels
