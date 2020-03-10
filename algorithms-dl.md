---
title: algorithms-dl
description: overview of main groups of deep learning algorithms
published: 1
date: 2020-03-10T11:16:09.549Z
tags: 
---

## Deep learning?

According to [Wikipedia](https://en.wikipedia.org/wiki/Deep_learning): “Deep learning (also known as deep structured learning or differential programming) is part of a broader family of machine learning methods based on artificial neural networks with representation learning. Learning can be supervised, semi-supervised or unsupervised”.

**a collection of algorithms inspired by the workings of the human brain in processing data and creating patterns for use in decision making, which are expanding and improving on the idea of a single model architecture called Artificial Neural Network(ANN)**.

## Convolutional Neural Networks (CNN)

Convolutional Neural Networks employ a function called [convolution](https://theaisummer.com/Neural_Network_from_scratch_part2/) The concept behind them is that instead of connecting each neuron with all the next ones, we connect it with only a handful of them (the receptive field).

In a way, they try to regularize feedforward networks to avoid overfitting (when the model learns only pre-seen data and can’t generalize), which makes them very good in identifying spatial relationships between the data.

![convolutional-neural-network](https://theaisummer.com/assets/img/posts/convolutional-neural-network.png)

That’s why their primary use case is Computer Vision and applications such as image classification, video recognition, medical image analysis and [self-driving cars](https://theaisummer.com/Self_driving_cars/) where they achieve literally superhuman performance.

They are also ideal to combine with other types of models such as Recurrent Networks and Autoencoders. One such example is [Sign Language Recognition](https://theaisummer.com/Sign-Language-Recognition-with-PyTorch/).

## Recurrent Neural Networks (RNN)

Recurrent networks are perfect for time-related data and they are used in time series forecasting. They use some form of feedback, where they return the output back to the input. You can think of it as a loop from the output to the input in order to pass information back to the network. Therefore, they are capable to remember past data and use that information in its prediction.

To achieve better performance researchers have modified the original neuron into more complex structures such as [GRU units](https://www.coursera.org/lecture/nlp-sequence-models/gated-recurrent-unit-gru-agZiL) and [LSTM Units](https://theaisummer.com/Bitcon_prediction_LSTM/). LSTM units have been used extensively in natural language processing in tasks such as language translation, speech generation, text to speech synthesis.

![lstm_cll](https://theaisummer.com/assets/img/posts/lstm_cll.jpg)

## Recursive Neural Network

Recursive Neural Networks are another form of recurrent networks with the difference that they are structured in a tree-like form. As a result, they can model hierarchical structures in the training dataset.

They are traditionally used in NLP in applications such as Audio to text transcription and sentiment analysis because of their ties to binary trees, contexts, and natural-language-based parsers. However, they tend to be much slower than Recurrent Networks

## AutoEncoders

[Autoencoders](https://theaisummer.com/Autoencoder/) are mostly used as an unsupervised algorithm and its main use-case is dimensionality reduction and compression. Their trick is that they try to make the output equal to the input. In other works, they are trying to reconstruct the data.

They consist of an encoder and a decoder. The encoder receives the input and it encodes it in a latent space of a lower dimension. The decoder takes that vector and decodes it back to the original input.

![autoencoder](https://theaisummer.com/assets/img/posts/autoencoder.jpg)

That way we can extract from the middle of the network a representation of the input with fewer dimensions. Genius, right?

Of course, we can use this idea to reproduce the same but a bit different or even better data (training data augmentation, data denoising, etc)

## Deep Belief Networks and Restricted Boltzmann Machines

[Restricted Boltzmann Machines](https://towardsdatascience.com/restricted-boltzmann-machines-simplified-eab1e5878976) are stochastic neural networks with generative capabilities as they are able to learn a probability distribution over their inputs. Unlike other networks, they consist of only input and hidden layers( no outputs).

In the forward part of the training the take the input and produce a representation of it. In the backward pass they reconstruct the original input from the representation. (Exactly like autoencoders but in a single network).

![restricted-boltzmann-machine](https://theaisummer.com/assets/img/posts/restricted-boltzmann-machine.png)

Multiple RBM can be stacked to form a [Deep Belief Network](http://deeplearning.net/tutorial/DBN.html). They look exactly like Fully Connected layers, but they differ in how they are trained. That’s because they train layers in pairs, following the training process of RBMs (described before)

However, DBNs and RBMs have kind of abandoned by the scientific community in favor of Variational Autoencoders and GANs

## Generative Adversarial Networks (GAN)

[GANs](https://theaisummer.com/Generative_Artificial_Intelligence/) were introduced in 2016 by Ian Goodfellow and they are based on a simple but elegant idea: You want to generate data, let’s say images. What do you do?

You build two models. You train the first one to generate fake data (generator) and the second one to distinguish real from fakes ones(discriminator). And you put them to compete against each other.

The generator becomes better and better at image generation, as its ultimate goal is to fool the discriminator. The discriminator becomes better and better at distinguish fake from real images, as its goal is to not be fooled. The result is that we now have incredibly realistic fake data from the discriminator.

![generative-adversarial-networks](https://theaisummer.com/assets/img/posts/generative-adversarial-networks.png)

Applications of Generative Adversarial Networks include video games, astronomical images, interior design, fashion. Basically, if you have images in your fields, you can potentially use GANs. Oooh, do you remember Deep Fakes? Yeah, that was all made by GANs.

## Transformers

[Transformers](https://ai.googleblog.com/2017/08/transformer-novel-neural-network.html) are also very new and they are mostly used in language applications as they are starting to make recurrent networks obsolete. They based on a concept called attention, which is used to force the network to focus on a particular data point.

Instead of having overly complex LSTM units, you use Attention mechanisms to weigh different parts of the input based on their significance. [The attention mechanism](https://lilianweng.github.io/lil-log/2018/06/24/attention-attention.html) is nothing more than another layer with weights and its sole purpose is to adjust the weights in a way that prioritizes segments of inputs while deprioritizing others.

Transformers, in fact, consist of a number of stacked encoders (form the encoder layer), a number of stacked decoders (the decoder layer) and a bunch of attention layers (self- attentions and encoder-decoder attentions)

![transformers](https://theaisummer.com/assets/img/posts/transformers.png)

Transformers are designed to handle ordered sequences of data, such as natural language, for various tasks such as machine translation and text summarization. Nowadays BERT and GPT-2 are the two most prominent pretrained natural language systems, used in a variety of NLP tasks, and they are both based on Transformers.

## Graph Neural Networks

Unstructured data are not a great fit for Deep Learning in general. And there are many real-world applications where data are unstructured and organized in a graph format. Think social networks, chemical compounds, knowledge graphs, spatial data.

[Graph Neural Networks](https://theaisummer.com/Graph_Neural_Networks/) purpose is to model Graph data, meaning that they identify the relationships between the nodes in a graph and produce a numeric representation of it. Just like an embedding. So, they can later be used in any other machine learning model for all sorts of tasks like clustering, classification, etc.

## Deep Learning in Natural Language Processing (NLP)

### Word Embeddings

Word Embeddings are the representations of words into numeric vectors in a way that capture the semantic and syntactic similarity between them. This is necessary because neural networks can only learn from numeric data so we had to find a way to encode words and text into numbers.

*   [Word2Vec](https://pathmind.com/wiki/word2vec) is the most popular technique and it tries to learn the embeddings by predicting a word based on its context (CBOW**)** or by predicting the surrounding words based on the word (Skip-Gram). Word2Vec is nothing more than a simple neural network with 2 layers that has words as inputs and outputs. Words are fed to the Neural Network in the form of one-hot encoding.

    In the case of CBOW, the inputs are the adjacent words and the output is the desired word. In the case of Skip-Gram, it’s the other way around.

*   [Glove](https://medium.com/@jonathan_hui/nlp-word-embedding-glove-5e7f523999f6) is another model that extends the idea of Word2Vec by combining it with matrix factorization techniques such as Latent Semantic Analysis, which are proven to be really good as global text statistics but unable to capture local context. So the union of those two gives us the best of both worlds.

*   [FastText](https://research.fb.com/blog/2016/08/fasttext/) by Facebook utilizes a different approach by making use of character-level representation instead of words.

*   **Contextual Word Embeddings** replace Word2Vec with Recurrent Neural Networks to predict, given a current word in a sentence, the next word. That way we can capture long term dependencies between words and each vector contains both the information on the current word and on the past ones. The most famous version is called [ELMo](https://allennlp.org/elmo) and it consists of a two-layer bi-directional LSTM network.

*   [Attention Mechanisms](https://blog.floydhub.com/attention-mechanism/) and Transformers are making RNN’s obsolete (as mentioned before), by weighting the most related words and forgetting the unimportant ones.

### Sequence Modeling

Sequence models are an integral part of Natural Language Processing as it appears on lots of common applications such as [Machine Translation](https://www.tensorflow.org/tutorials/text/nmt_with_attention), Speech Recognition, Autocompletion and Sentiment Classification. Sequence models are able to process a sequence of inputs or events such as a document of words.

For example, imagine that you want to translate a sentence from English to French.

To do that you need a [Sequence to Sequence model (seq2sec)](https://blog.keras.io/a-ten-minute-introduction-to-sequence-to-sequence-learning-in-keras.html). Seq2sec models include an encoder and a decoder. The encoder takes the sequence(sentence in English) and produces an output, a representation of the input in a latent space. This representation is fed to the decoder, which gives us the new sequence (sentence in France).

The most common architectures for encoder and decoder are Recurrent Neural Networks (mostly LSTMs) because they are great in capturing long term dependencies and Transformers that tend to be faster and easier to parallelize. Sometimes they are also combined with Convolutional Networks for better accuracy.

[BERT](https://github.com/google-research/bert) and [GPT-2](https://openai.com/blog/better-language-models/) are considered the two best language models and they are in fact Transformer based Sequence models .

## Deep Learning in Computer Vision

![cv_tasks](https://theaisummer.com/assets/img/posts/cv_tasks.jpg)

### Localization and Object Detection

[Image Localization](https://theaisummer.com/Localization_and_Object_Detection/) is the task of locating objects in an image and mark them with a bounding box, while object detection includes also the classification of the object.

The interconnected tasks are tackled by a fundamental model (and its improvements) in Computer Vision called R-CNN. RCNN and it’s predecessors Fast RCNN and Faster RCNN take advantage of regions proposals and Convolutional Neural Network.

An external system or the network itself( in the case of Faster RCNN) proposes some regions of interest in the form of a fixed-sized box, which might contain objects. These boxes are classified and corrected via a CNN (such as AlexNet), which decided if the box contains an object, what the object is and fixes the dimensions of the bounding box.

### Single-shot detectors

![yolo_app](https://theaisummer.com/assets/img/posts/yolo_app.jpg)

Single-shot detectors and it’s most famous member [YOLO (You Only Look Once)](https://theaisummer.com/YOLO/) ditch the idea of region proposals and they use a set of predefined boxes.

These boxes are forwarded to a CNN, which predicts for each one a number of bounding boxes with a confidence score, it detects one object centered in it and it classifies the object into a category. In the end, we keep only the bounding boxes with a high score.

Over the years YOLOv2, YOLOv3, and YOLO900 improved on the original idea both on speed and accuracy.

### Semantic Segmentation

![semseg](https://theaisummer.com/assets/img/posts/semseg.jpg)

One of the fundamentals tasks in computer vision is the classification of all pixels in an image in classes based on their context, aka [Semantic Segmentation](https://theaisummer.com/Semantic_Segmentation/). In this direction, Fully Convolutional Networks (FCN) and U-Nets are the two most widely-used models.

*   **Fully Convolutional Networks (FCN)** is an encoder-decoder architecture with one convolutional and one deconvolutional network. The encoder downsamples the image to capture semantic and contextual information while the decoder upsamples to retrieve spatial information. That way we manage to retrieve the context of the image with the smaller time and space complexity possible.

*   **U-Nets** are based on the ingenious idea of skip-connections. Their encoder has the same size as the decoder and skip-connections transfer information from the first one to the latter in order to increase the resolution of the final output.

### Pose Estimation

[Pose Estimation](https://www.fritz.ai/pose-estimation/) is the problem of localizing human joints in images and videos and it can either be 2D or 3D. In 2D we estimate the (x,y) coordinates of each joint while in 3D the (x,y,z) coordinates.

[PoseNet](https://github.com/tensorflow/tfjs-models/tree/master/posenet) dominates the field (it’s the go-to model for most smartphone applications) and it uses Convolutional Neural Networks (didn’t see that coming, did you?). We feed the image to a CNN and we use a single-pose or a multi-pose algorithm to detect poses. Each pose is associated with a confidence score and some key points coordinates. In the end, we keep the ones with the highest confidence score.