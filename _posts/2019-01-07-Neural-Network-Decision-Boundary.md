---
title: Neural Network Decision Boundary
layout: post
date: 2019-01-07 10:20
image: /assets/images/NeuralNetBoundary/decision-boundary.png
headerImage: true
tag:
- machine learning
- keras
- tensorflow
- neural networks
- tutorial

star: false
category: blog
author: Rohit Midha
---

<p style="font-size:12px;">Inspired by Jon Char's Publication.</p>
# Objective

In this post I will implement an example neural network using Keras and show you how the Neural Network learns over time.
Keras is a framework for building ANNs that sits on top of either a Theano or TensorFlow backend.
I really like Keras cause it's fairly simply to use and one can get a network up and running in no time.
The [Keras Blog](https://blog.keras.io/) has some great examples of how to use the framework.

---

Start off by importing all the required packages


```python
import numpy as np
np.random.seed(0)
from sklearn import datasets
import matplotlib.pyplot as plt
%matplotlib inline

from keras.models import Sequential
from keras.layers import Dense
from keras.optimizers import SGD
```

Next we generate the dataset and the scatter plot.


```python
X, y = datasets.make_moons(n_samples=1000, noise=0.1, random_state=0)
colors = ['blue' if label == 1 else 'red' for label in y]
plt.scatter(X[:,0], X[:,1], color=colors)
y.shape, X.shape
```




    ((1000,), (1000, 2))




![png](/assets/images/NeuralNetBoundary/output_3_1.png)


## Defining the Model
The Keras Python library makes creating deep learning models fast and easy.

The sequential API allows you to create models layer-by-layer for most problems. Keras has different activation functions built in such as 'sigmoid', 'tanh', 'softmax', and [many others](https://keras.io/optimizers/). Also built in are different weight initialization options. We use the sigmoid activation which limits the values to $[-\epsilon,\epsilon]$

This initialization method corresponds to the `'glorot_uniform'` initialization option in Keras.


```python
# Define our model object
model = Sequential()

# kwarg dict for convenience
layer_kw = dict(activation='sigmoid', init='glorot_uniform')

# Add layers to our model
model.add(Dense(output_dim=5, input_shape=(2, ), **layer_kw))
model.add(Dense(output_dim=5, **layer_kw))
model.add(Dense(output_dim=1, **layer_kw))
```


## Defining the Optimizer
While initializing the Keras model we also need to specify an optimizer such as SGD or Adam or RMSProp. In this case we will use SGD. You can however read more about them [here](https://keras.io/optimizers/).


```python
sgd = SGD(lr=0.001)
```

## Compile the Model
A loss function (or objective function, or optimization score function) is one of the two parameters required to compile a model, the other being the optimizer itself.



```python
model.compile(optimizer=sgd, loss='binary_crossentropy')
```

## Summarize the Model
Keras allows for models to be summarized using `model.summary()`.



```python
model.summary()
```
>
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    dense_4 (Dense)              (None, 5)                 15        
    _________________________________________________________________
    dense_5 (Dense)              (None, 5)                 30        
    _________________________________________________________________
    dense_6 (Dense)              (None, 1)                 6         
    =================================================================
    Total params: 51
    Trainable params: 51
    Non-trainable params: 0
    _________________________________________________________________
>

## Train the Model
We can now train our model using the `model.fit()` method. We will save this as history to refer to it at a future point. Since the number of epochs is very high we will set `verbose=0` and shuffle the data as well.



```python
history = model.fit(X[:500], y[:500], verbose=0, nb_epoch=4000, shuffle=True)
```

## Visualizing the Results


```python
def plot_decision_boundary(X, y, model, steps=1000, cmap='Paired'):
    cmap = plt.get_cmap(cmap)

    # Define region of interest by data limits
    xmin, xmax = X[:,0].min() - 1, X[:,0].max() + 1
    ymin, ymax = X[:,1].min() - 1, X[:,1].max() + 1
    steps = 1000
    x_span = np.linspace(xmin, xmax, steps)
    y_span = np.linspace(ymin, ymax, steps)
    xx, yy = np.meshgrid(x_span, y_span)

    # Make predictions across region of interest
    labels = model.predict(np.c_[xx.ravel(), yy.ravel()])

    # Plot decision boundary in region of interest
    z = labels.reshape(xx.shape)

    fig, ax = plt.subplots()
    ax.contourf(xx, yy, z, cmap=cmap, alpha=0.5)

    # Get predicted labels on training data and plot
    train_labels = model.predict(X)
    ax.scatter(X[:,0], X[:,1], c=y, cmap=cmap, lw=0)

    return fig, ax
```

```python
plot_decision_boundary(X, y, model, cmap='RdBu')
```
![png](/assets/images/NeuralNetBoundary/decision-boundary.png)

---

<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/RohitMidha23" data-size="large" data-show-count="true" aria-label="Follow @RohitMidha23 on GitHub">Follow @RohitMidha23</a>
<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>



Show some :heart: by :star:ing it.


<!-- Place this tag where you want the button to render. -->
<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/RohitMidha23/Neural-Network-Decision-Boundary" data-size="large" data-show-count="true" aria-label="Star RohitMidha23/Neural-Network-Decision-Boundary on GitHub">Star</a>
<a href="https://github.com/RohitMidha23/Neural-Network-Decision-Boundary" class="github-corner" aria-label="View source on GitHub"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#fff; color:#151513; position: absolute; top: 0; border: 0; left: 0; transform: scale(-1, 1);" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>
