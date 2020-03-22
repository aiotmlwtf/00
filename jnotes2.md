---
title: notes2
description: 
published: 1
date: 2020-03-22T19:37:26.400Z
tags: 
---



Optimization algorithms are the ‘backbone algorithms’ of Machine Learning.

<details>
<summary>some definitions</summary>
		
An **Optimization algorithm** is executed a predefined number of times and is used to find optimal solutions to problems, in mathematical terms, these ‘problems’ are referred to as functions.
		
**Gradient Descent** is an optimization algorithm used to find values that reduce the cost function.  This is done through the calculation of a gradient value, that is utilized to select values at each step that finds the local minimum of a cost function. The negative of the gradient is used to find the local minimum.
		
The **Cost function** quantifies ‘how well’ a machine learning model performs. The quantification is an output(cost) based on a set of inputs, which are referred to as parameter values. The parameter values are used to estimate a prediction, and the ‘cost’ is the difference between the prediction and the actual values.
		


The smallest parameter values that lie within the entire domain of a cost function
is called a **Global Minimum**. A **local minimum** refers to the lowest parameter values that lie within a set range of the cost function.

**Convergence** describes the notion of movement towards optimal parameter values or global minimum when used in the context of machine learning.

An **activation function** (also: ‘squashing function’) is a mathematical operation that transforms the result or signals of neurons into a normalized output. The purpose of an activation function as a component of a neural network is to introduce non-linearity within the network. The inclusion of an activation function enables the neural network to have greater representational power and solve complex functions.

**common activation functions**
- Sigmoid function
- ReLU
- Softmax function
- ReLU (Rectified Linear Unit)

A type of activation function that transforms the value results of a neuron.
The transformation imposed by ReLU on values from a neuron is represented by the formula y=max(0,x). The ReLU activation function clamps down any negative values from the neuron to 0, and positive values remain unchanged. The result of this mathematical transformation is utilized as the output of the current layer and used as input to a consecutive layer within a neural network.
In the matter of Vanishing gradient, ReLU is a standard solution to limiting or avoiding the effect of vanishing gradient on a neural network.

**Softmax**
A type of activation function that is utilized to derive the probability distribution of a set of numbers within an input vector.
</details>
  
<details>
<summary>Gradient Descent</summary>

Gradient Descent is a very common optimization algorithm, and most likely, the first optimization algorithm a lot of Machine learning engineers and Data scientists are introduced to.
Let's paint a picture. We have a cost function, and we need to find the optimum solution to solve the cost function. Here comes gradient descent, an algorithm that works by making changes to the values of the parameters that are within the model, all in the purpose of minimizing the cost function. An example of a cost function is [Mean Squared Error](https://en.wikipedia.org/wiki/Mean_squared_error).

Gradient descent intrinsic functionality works by finding the direction to take towards a local minimum based on the calculated gradient obtained from the error function with respect to the parameters at a particular data point.
It might help to understand gradient descent with some imagery and visualization.
Let’s use a graph that contains a bowl-shaped curve, and a ball, placed on the top left side of the curve. The ball represents a certain point (value) in the parameter space that is initially randomly chosen, and the curve represents the cost values plotted against a range of parameter values. The goal is to reach the parameter value that provides the lowest cost value.
On the x-axis of the plot is a value representing the cost, and on the y-axis is a value denoted by ‘X’ that represents the range of parameter values that we are utilizing to solve the cost function.
￼
￼
Image of a cost function curvature
The minimum (singular)/minima(plural) is a point within the slope where the optimum value that minimizes the cost function exists, and gradient descent is the algorithm that guides our ball towards the minimum at several steps (iterations).
To solve the cost function, we are looking for the lowest point of the curve, and this is the point where the gradient is zero or close to zero.
Quick note: Cost function curve aren’t always necessarily a nice bowl shape with one local minima. In the example used in the image above there is only one input paramter(1 dimensional paramter space) to the cost fucntion, but in practice, the parameter space tends to have more dimensions.

**Batch Gradient Descent**
  
We understand how gradient descent works and can now apply it to our training data. The application of the gradient descent algorithm to training data comes in various forms. One form is called Batch Gradient Descent (BGD).
In the image above, we take steps towards a local minimum. In BGD, we actually utilize every training data at our disposal to decide as to which direction and by how much we move towards a minimum. We use all our training data at each step.
For extensive training data, the training process can be prolonged but can be computationally efficient as we do not make any changes to our model parameters as often as other variants of gradient descent.
Although BGD is not memory efficient, as you can imagine that we require all our datasets available in memory when training a model.

**Stochastic Gradient Descent**
  
On the other side of the coin to BGD, we have Stochastic Gradient Descent (SGD).
As opposed to iterating through every data within our training set and then making a step towards a local minimum, SGD works by actually picking a single data point from the training set and computing the gradient, based on this single data point.
You can probably tell that between BGD and SGD, SGD is the faster algorithm since you are computing the gradient based on a single instance of the data as opposed to the entire dataset, but at what cost.

Updates made within the parameter space during gradient descent can be noisy when using SGD. The noisiness characteristic of SGD is a result of its random nature that occurs when selecting data points from the training set to compute gradients from at each step. To accommodate for the noisiness nature of SGD and ensure we reach an optimum parameter value, we have to iterate over the training data a certain number of times and ensure that at the beginning of the gradient descent process, the training data is shuffled. Noise leads to ambiguous parameter values to solve the cost function, although given enough time, SGD will approach a local minimum. The noisiness and random nature of SGD are also beneficial. It’s useful for when the algorithm gets ‘stuck’ in a local minimum that isn’t the global minimum. In comparison to BGD, SGD has the benefit of escaping local minimums and finding the global minimum due to its random and erratic nature when allocating parameter values at each step.

But BGD parameter values are closer to the global minimum and optimal in comparison to SGD. There is a trade-off between speed and optimality when faced with selecting between both variants of the gradient descent algorithms.

**Mini Batch Gradient Descent**

How about an approach that leverages the good characteristics of both SGD and BGD.
Mini Batch Gradient Descent computes the gradient based on randomly selected data within the training set just like SGD but does not include the entire dataset when computing gradients, so it’s also not quite BGD. You could say it’s a hybrid.
Mini Batch GD uses a small number of data when computing gradients; in comparison to BGD, it’s faster, but when compared to SGD, it’s still slower. The advantage of Mini Batch GD to SGD is the reduction in noise within the parameter space. This means that utilizing Mini Batch GD, means optimum parameter values are more reachable.
</details>