---
title: glossary
description: terms and acronyms, in alphabetical order
published: 1
date: 2020-03-06T21:50:01.189Z
tags: 
---

New insights and (re-)definitions pop up quite often in the field of AI/ML. 
Let's collect usefull ones, please <span style="background-color:#fcc; color:#f00;">add any definition that you deem constructive below</span>:


## acronyms
BOYB - Bring Your Own Blowtorch
BOYT - Bring Your Own Topic
CNN - Convolutional Neural Network
DRY - Don't Repeat Yourself
GA - Genetic Algorithm
GANN - Generative Adverserial Neural Network
KISS - Keep It Simple Stupid
LAM - Learning About Machines
LSTM - Long Short Term Memory
RNN - Recurrent Neural Network
optimized to process time-series data
related: vanishing gradient problem, long short term memory (LSTM), Gates RNN
RTFE - Read The Fucking Error
RTFM - Read The Fucking Manual
TBC - To Be Continued
TBD - To Be Done
VAE - Variational Auto Encoder

## AI terms

**artificial intelligence (AI)**
- ~intelligent~ behaviour exhibited by machines
- the behaviour of a system that adapts its actions in response to its environment and prior experience
- “The theory and development of computer systems able to perform tasks normally requiring human intelligence.” - Oxford English Dictionary

**artificial general intelligence (AGI)**
- human-level intelligence: have the capacity to understand or learn any intellectual task that a human being can
- primary goal of some artificial intelligence research and a common topic in science fiction and futures studies.

**artificial neural networks (ANN/NN)**
- learning mechanism is modelled on the behaviour of a biological brain
- input signals are modified as they pass through networked layers of neurons before emerging as an output
- experience is encoded by varying the strength of interactions between neurons in the network
- the basic model behind many deep learning techniques

(multi-layer) perceptron, activation, gradient descent, back-propagation, training


**applied AI / weak AI**
- specific problem solving or reasoning tasks, does not attempt to perform the full range of human cognitive abilities

**strong AI (narrow AI)**
- perform the full range of human cognitive abilities, eg. experience consciousness


## ML terms

**machine learning (ML)**
- broad category of approaches to endow a machine with artificial intelligence
- the process by which a system learns from a training set so that it can deliver autonomously an appropriate response to new data
- uses statistical techniques to give computer systems the ability to “learn” (i.e., progressively improve performance on a specific task) from some data, without being explicitly programmed
...


**deep learning (DL)**
- “deep” in deep learning refers to having more than one hidden layer of neurons in a neural network
- both supervised and unsupervised learning can be used for training
- derived associations/patterns/'concepts' are:
	- mostly unknown (probably unknowable) by humans, as they're hidden inside the network
	- meaningless to us, these are abstract machine-associations, not real-life/human concepts
	- not formally verifiable (the model cannot be proven to be correct) 

This can be(-come) very problematic in science (correctness). Depending on the domain, their application in society raises ethical questions concerning liability and agency, especially in a decision-making process without human involvement/intervention. Researchers in the humanities/law concern themselves with such questions, but sometimes the 'industry' [raises awareness as well](https://futureoflife.org/ai-open-letter/).


**bayesian learning**

- enables encoding our initial perception of what a model should look like, regardless of what the data tells, useful when there’s a sparse amount of data to train a model properly
- bayesian network: probabilistic graphical model representing a group of variables along with their conditional dependencies through a direct acyclic graph; it is also used to compute the probability distribution for a subset of network variables, provided the distributions or values of any subset of the remaining variables

**clustering**

grouping of data instances or objects with similar features and characteristics

**decision tree**

construct that uses a tree like graph or model of decisions and their possible consequences,including chance event outcomes,resource costs and utility.

**deductive learning**

from a known general rule to a new rule that is logically entailed (and thus nothing new), but is nevertheless useful because it allows more efficient processing

**inductive learning**

from a set of specific input-output pairs to a (possibly incorrect) general rule is called inductive learning.

**depth-first search**
traversal of a graph or a tree data structure; 
starts from the root node and traverses as far as possible for each branch before backtracking

**hidden markov model**
HMM is a temporal probabilistic model in which the state of the process is described by a single discrete random variable


**validation set**
A part of the dataset that is used to tune the parameters of a machine learning model. It can also be used to determine a stopping point for the back-propagation algorithm


**softmax function**
mathematical function often used for classification
calculates the probability distribution of one class, over all the available classes (summation: over all classes):

$$
F(X) = exp(X) / summation(exp(X))
$$

$$
F(X) = { sigma(X) = 1/(1+exp(-X)) }
$$


