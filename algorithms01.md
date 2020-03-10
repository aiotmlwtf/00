---
title: algorithms 01
description: ML algorithm types
published: 1
date: 2020-03-10T11:18:25.486Z
tags: algorithm
---

This is a general overview, for more specific implementations/functions, look [here](/algorithms02)


# ML /


type of learning:

**supervised
semi-supervised
unsupervised
reinforcement learning**

<div style="background-color:#eee;">

![ml_algo_overview1_alpha.png](/ml_algo_overview1_alpha.png)
</div>
  
  
## supervised learning
Make predictions based on a set of examples training happens with labeled data sets that have inputs and expected outputs.

### regression** [Linear, Polynomial, Nonparametric]
Predict a numerical value given some input: “How much money would a bank gain (lose) by lending to a certain client?” Used for pricing optimization, modeling historical sales in order to determine a pricing strategy and predict demand for products that have not been sold before. The concept of regression was first described in 1875 (Francis Galton).
### classification [Naive Bayes, k-NN,SVM, Random Forest, Neural Networks] 
specify which of k categories some input belongs to. “Will a client be able to pay his loan back?” Used for e-mail spam filtering, bank customers loan pay back willingness prediction, cancer tumour cells identification, sentiment analysis, drugs classification, facial keypoints detection, and pedestrians detection in an automotive car driving.
### forecasting [Trending, Time-Series Modeling, Neural Networks]
generate predictions based on available data. Forecasting models are the bread and butter in business intelligence.
### ranking [HITS, SALSA, PageRank]
rank (i.e., produce a permutation of items in new, unseen lists) in a way that is similar to the rankings in the training data. “What are the top 10 world’s safest banks?” Used in bioinformatics, drug discovery, information retrieval, sentiment analysis, machine translation, and online advertising. 

## unsupervised learning
Discover intrinsic patterns that underlie the data (which is totally unlabeled), such as a clustering structure, a low- dimensional manifold, or a sparse tree and graph. Used in healthcare and pharma for such tasks as human genetic clustering and genome sequence analysis. They are also widely used across all industries for customers segmentation, recommender systems, chatbots, topic modeling, anomalies detection, grouping of shopping items, search results grouping, etc.
### clustering [k-means, Mean-Shift, Hierarchical, Fuzzy c-means]
group the similar kind of data items by considering the most satisfied condition: all the items in the same group (called a cluster) are more similar to each other than to the items in the other groups (clusters) 
### anomalies detection [Density-Based, SVM- Based, Clustering-Based] 
algorithm sifts through a set of events or objects and flags some of them as unusual or atypical
### dimensionality reduction [PCA, Singular Value Decomposition, LDA]
algorithm is asked to reduce the number of random variables under consideration by obtaining a set of principal variables. Dimensionality reduction can be divided into feature selection and feature extraction
### missing data imputation [mean imputation, k-NN] 
the algorithm given examples with some missing entries, provide the values of the missing entries
### association rules learning [AIS, SETM, APRIORI, FP-GROWTH]
a rule-based method for discovering interesting relations between variables in large databases. It is intended to identify strong rules discovered in databases using some measures of interestingness. 



## reinforcement learning
Try out scenarios to discover which actions yield the greatest reward. Rather than being told which actions to take, learn optimal sequence of actions from successful and failed attempts. Analyze and optimize the behavior of -and based on- feedback from the environment.
 
### Q-learning 
based on a mathematical optimization method known as dynamic programming. Given current states of a system, the algorithm finds an optimal policy (i.e., set of actions) that maximizes Q-value function. 
The Q-learning algorithm is able to learn an optimal stock market trading strategy with a single instruction: maximize the value of a portfolio.
### Deep Q Network
leverages a Neural Network to estimate the Q-value function. It resolves some limitations of the Q-learning algorithm. Deep Deterministic Policy Gradient — the algorithm is designed for such problems as physical control tasks, where the action space is continuous. 
### State-Action-Reward-State-Action 
resembles Q-learning, but learns Q-value based on the action performed by the current policy instead of the greedy policy. 

Robots use deep reinforcement learning to pick a device from one box and put it in a container. RL algorithms reduce transit time for stocking and retrieving products in the warehouse to optimize space utilization and warehouse operations. Used in operational research and logistics, split delivery vehicle routing, credit assignment, multi-armed bandits.

---
