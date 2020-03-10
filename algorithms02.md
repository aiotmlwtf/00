---
title: algorithms02
description: specific ML-related functions/models/algorithms/networks
published: 1
date: 2020-03-10T11:20:07.213Z
tags: 
---

Here are specific implementations/functions.

For a general overview, look [here](/algorithms01)
For an overview of **deep learning algorithms**, look [here](/algorithms-dl)

### Backpropagation

Neural Networks are able to learn the desired function using big amounts of data and an iterative algorithm called [backpropagation](https://brilliant.org/wiki/backpropagation/). We feed the network with data, it produces an output, we compare that output with a desired one (using a loss function) and we readjust the weights based on the difference.

And repeat. And repeat. The adjustment of weights is performed using a non-linear optimization technique called [stochastic gradient descent](https://ruder.io/optimizing-gradient-descent/).

After a while, the network will become really good at producing the output. Hence, the training is over. Hence, we manage to approximate our function. And if we pass an input with an unknown output to the network, it will give us an answer based on the approximated function.

Let’s use an example to make this clearer. Let’s say that for some reason we want to identify images with a tree. We feed the network with any kind of images and it produces an output. Since we know if the image has actually a tree or not, we can compare the output with our truth and adjust the network.

As we pass more and more images, the network will make fewer and fewer mistakes. Now we can feed it with an unknown image, and it will tell us if the image contains a tree.

Over the years researchers came up with amazing improvements on the original idea. Each new architecture was targeted on a specific problem and one achieved better accuracy and speed. We can classify all those new models in specific categories:

## Feedforward Neural Networks (FNN)

Feedforward Neural Networks are usually [fully connected](https://theaisummer.com/Neural_Network_from_scratch/), which means that every neuron in a layer is connected with all the other neurons in the next layers. The described structure is called Multilayer Perceptron and originated back in 1958\. Single-layer perceptron can only learn linearly separable patterns, but a multilayer perceptron is able to learn non-linear relationships between the data.

![neural-network](https://theaisummer.com/assets/img/posts/neural-network.png)

They are exceptionally well on tasks like classification and regression. Contrary to other machine learning algorithms, they don’t converge so easily. The more data they have, the higher their accuracy.

## functions

fitness function (GA)
activation function (NN)
sigmoid
[softmax](/softmax)
back-propagation 
converging
over-fitting
inference

## networks/models

**clustering**
grouping of data instances or objects with similar features and characteristics

**decision tree**
construct that uses a tree like graph or model of decisions and their possible consequences,including chance event outcomes,resource costs and utility.

**depth-first search**
traversal of a graph or a tree data structure; starts from the root node and traverses as far as possible for each branch before backtracking

**hidden markov model (HMM)**
a temporal probabilistic model in which the state of the process is described by a single discrete random variable

**bayesian network**
probabilistic graphical model representing a group of variables along with their conditional dependencies through a direct acyclic graph; it is also used to compute the probability distribution for a subset of network variables, provided the distributions or values of any subset of the remaining variables

**Convolutional Neural Network (CNN)**
process images, training a convolutional neural network to detect objects
**related:** image convolution, LeNet, AlexNet, VGGNet, GoogLeNet, ResNet, image datasets, cnn performance, image segmentation, UNet, GapNet, GAN
