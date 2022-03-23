---
title: Pytorch - Simple Linear Regression
layout: post
date: 2020-04-26 12:20
image: /assets/images/PytorchLinearRegression/logo.png
headerImage: true
tag:
- machine learning
- pytorch
- tutorial

star: false
category: blog
author: Rohit Midha
---

This is the fourth tutorial of the Explained! series and the start of the Pytorch tutorials.

I will be cataloging all the work I do with regards to PyLibraries and will share it here or on [my Github](http://bit.ly/RohitMidha23GitHub).

That being said, Dive in!



```python
# Necessary imports
import torch
import numpy as np
import matplotlib.pyplot as plt
```


```python
# Create the sample dataset
X = np.array([1.0, 20.4, 30.5, 7.5, 9.9,
              100.9, 200.1, 45.1, 150.1, 7.0,
              29.4, 31.5, 157.3, 10.9, 120.6,
              16.9, 201.1, 21.1, 300.1, 21.0,
              120.4, 230.5, 37.5, 49.9, 230.0,
              109.9, 121.1, 145.1, 157.1, 17.0,
              219.4, 131.5, 187.3, 210.9, 290.6,
              126.9, 71.1, 91.1, 19.1, 100.0])
X_train = []
# normalize each value
for i in X:
  X_train.append([i/100])

X_train = np.array(X_train)

y_train = np.array([i*0.175 + 0.4 for i in X_train]) # bias should be 0.4 and w=0.175
```


```python
# Check the shape of the data to be sure
print(X_train.shape)
print(y_train.shape)
```

    (40, 1)
    (40, 1)



```python
# Visualize the data
plt.scatter(X_train, y_train, c="green", label="Original Data")
plt.show()
```


![png](/assets/images/PytorchLinearRegression/output_3_0.png)



```python
# Create the torch tensors
X = torch.from_numpy(X_train)
y = torch.from_numpy(y_train)
```


```python
print(X.shape)
print(y.shape)
```

    torch.Size([40, 1])
    torch.Size([40, 1])



```python
# Define the parameters needed
input_size = 1
hidden_layers = 1
outputs = 1
learning_rate = 0.001
num_epochs = 150
```


```python
# Create the first weight tensor
w1 = torch.rand(input_size, hidden_layers, requires_grad=True)
print(w1.shape)
```

    torch.Size([1, 1])



```python
b1 = torch.rand(hidden_layers, outputs, requires_grad=True)
print(b1.shape)
```

    torch.Size([1, 1])



```python
for i in range(1, num_epochs):
  # y = wx + b - one forward pass
  y_pred = X.mm(w1.double()).clamp(min=0).add(b1.double())
  # Here the `.clamp(min=0)` works as the ReLu actiation function

  # calculate the loss
  loss = (y-y_pred).pow(2).sum()

  if i % 25==0:
    print("Epoch : ", i, "\t Loss :", loss)

  # backpropogation
  loss.backward()

  with torch.no_grad():
    # update the weights and biases
    w1 -= (learning_rate * w1.grad)
    b1 -= (learning_rate * b1.grad)
    # set the gradients to 0
    w1.grad.zero_()
    b1.grad.zero_()
```

    Epoch :  25 	 Loss : tensor(0.0021, dtype=torch.float64, grad_fn=<SumBackward0>)
    Epoch :  50 	 Loss : tensor(0.0004, dtype=torch.float64, grad_fn=<SumBackward0>)
    Epoch :  75 	 Loss : tensor(0.0001, dtype=torch.float64, grad_fn=<SumBackward0>)
    Epoch :  100 	 Loss : tensor(4.1570e-05, dtype=torch.float64, grad_fn=<SumBackward0>)
    Epoch :  125 	 Loss : tensor(1.3125e-05, dtype=torch.float64, grad_fn=<SumBackward0>)



```python
print(w1)
print(b1)
```

    tensor([[0.1753]], requires_grad=True)
    tensor([[0.3995]], requires_grad=True)


That's pretty close to the actual values we used.

You can try running with more iterations if you want to see if you ever get the actual values!


```python
# Let's visualize the output
plt.scatter(X, y, c="green", s=150, label="Original Data")
plt.plot(X, y_pred.detach().numpy(), label="Fitted Line")
plt.legend()
plt.show()
```


![png](/assets/images/PytorchLinearRegression/output_12_0.png)


As you can clearly see the line fits very well with the data.

This is a simple one neuron network that simply performs linear regression.

You might never use this in practice but the idea is to understand the concept!

---

<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/RohitMidha23" data-size="large" data-show-count="true" aria-label="Follow @RohitMidha23 on GitHub">Follow @RohitMidha23</a>
<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>

Find more at my Github repository [Explained](http://bit.ly/ExplainedRepo).

Show some :heart: by :star:ing it.

<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/RohitMidha23/Explained" data-size="large" data-show-count="true" aria-label="Star RohitMidha23/Explained on GitHub">Star</a>
<a href="http://bit.ly/2TGi2aE" class="github-corner" aria-label="View source on GitHub"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#fff; color:#151513; position: absolute; top: 0; border: 0; left: 0; transform: scale(-1, 1);" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>
