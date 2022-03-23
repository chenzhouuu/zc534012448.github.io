---
title: Data Visualization with Matplotlib
layout: post
date: 2019-01-30 11:20
image: /assets/images/MatplotlibExplained/pltlogo.png
headerImage: true
tag:
- matplotlib
- tutorial
- Explained

star: false
category: blog
author: Rohit Midha
---
This is the third tutorial of the Explained! series.

I will be cataloging all the work I do with regards to PyLibraries and will share it here or on [my Github](http://bit.ly/RohitMidha23GitHub).

I will also be updating this post as and when I work on Matplotlib.

That being said, Dive in!

# Data Visualization with Matplotlib

In the Python world, there are multiple tools for data visualizing:
* [**matplotlib**](http://matplotlib.org) produces publication quality figures in a variety of hardcopy formats and interactive environments across platforms; you can generate plots, histograms, power spectra, bar charts, errorcharts, scatterplots, etc., with just a few lines of code;
* [**Seaborn**](http://stanford.edu/~mwaskom/software/seaborn/index.html) is a library for making attractive and informative statistical graphics in Python;

and others (particularly, pandas also possesses with its own visualization funtionality).

Here, we will consider preferably matplotlib. Matplotlib is an excellent 2D and 3D graphics library for generating scientific, statistics, etc. figures. Some of the many advantages of this library include:

* Easy
* Great control of every element in a figure, including figure size and DPI.
* High-quality output
* GUI for interactively exploring figures.

## Working with Matplotlib


```python
import matplotlib.pyplot as plt
# This line configures matplotlib to show figures embedded in the notebook,
# instead of opening a new window for each figure. More about that later.
%matplotlib inline
import numpy as np
```

To create a simple line `matplotlib` plot you need to set two arrays for `x` and `y` coordinates of drawing points and them call the `plt.plot()` function.

pyplot is a part of the Matplotlib Package.
It can be imported like :
```python
    import matplotlib.pyplot as plt
```

Let's start with something cool and then move to the boring stuff, shall we?


### <em>The Waves</em>


```python
import numpy as np
import matplotlib.pyplot as plt
"""
numpy.arange([start, ]stop, [step, ]dtype=None)
    Return evenly spaced values within a given interval.
    Only stop value is required to be given.
    Default start = 0 and step = 1

"""
x = np.arange(0,5,0.1)
y = np.sin(x)
y2 = np.cos(x)
plt.plot(x, y)
plt.plot(x,y2)
plt.show()
```


![png](/assets/images/MatplotlibExplained/output_8_0.png)


## <em>Back to The Basics </em>

### Bar Charts

A diagram in which the numerical values of variables are represented by the height or length of lines or rectangles of equal width.


```python
objects = ('Python', 'C++', 'Java', 'Perl', 'Scala', 'Lisp')
x_pos = np.arange(len(objects)) # Like the enumerate function.
performance = [10,8,6,4,2,1] # Y values for the plot

# Plots the valueswith x_pos as X axis and Performance as Y axis
plt.bar(x_pos, performance)

# Change X axis values to names from objects
plt.xticks(x_pos, objects)

# Assigns Label to Y axis
plt.ylabel('Usage')

plt.title('Programming Language Usage')
plt.show()

```


![png](/assets/images/MatplotlibExplained/output_11_0.png)


### Pie Chart

A pie chart (or a circle chart) is a circular statistical graphic, which is divided into slices to illustrate numerical proportion.


```python
import matplotlib.pyplot as plt

# Data to plot
labels = ('Python', 'C++', 'Ruby', 'Java')
sizes = [10,16,14,11]

# Predefined color values
colors = ['gold', 'yellowgreen', 'lightcoral', 'lightskyblue']

# Highlights a particular Value in plot
explode = (0.1, 0, 0, 0)  # Explode 1st slice

# Plot
plt.pie(sizes, explode=explode, labels=labels, colors=colors)


plt.show()
```


![png](/assets/images/MatplotlibExplained/output_13_0.png)


### Line Chart

The statement:
```python
t = arange(0.0, 20.0, 1)
```
defines start from 0, plot 20 items (length of our array) with steps of 1.
We'll use this to get our X-Values for few examples.


```python
import matplotlib.pyplot as plt

t = np.arange(0.0, 20.0, 1)
s = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
plt.plot(t, s)

plt.xlabel('Item (s)')
plt.ylabel('Value')
plt.title('Python Line Chart')
plt.grid(True)
plt.show()
```


![png](/assets/images/MatplotlibExplained/output_16_0.png)



```python
import matplotlib.pyplot as plt

t = np.arange(0.0, 20.0, 1)
s = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
s2 = [4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23]
plt.plot(t, s)
plt.plot(t,s2)

plt.xlabel('Item (s)')
plt.ylabel('Value')
plt.title('Python Line Chart')
plt.grid(True)
plt.show()
```


![png](/assets/images/MatplotlibExplained/output_17_0.png)


Okay, now that that's taken care of, let's try something like $y =x^2$


```python
import matplotlib.pyplot as plt

a=[]
b=[]
# Try changing the range values to very small values
# Notice the change in output then
for x in range(-25000,25000):
    y=x**2
    a.append(x)
    b.append(y)

plt.plot(a,b)
plt.show()
```


![png](/assets/images/MatplotlibExplained/output_19_0.png)


## Subplots

Matplotlib allows for subplots to be added to each figure using it's Object Oriented API. All long we've been using a global figure instance. We're going to change that now and save the instance to a variable `fig`. From it we create a new axis instance `axes` using the `add_axes` method in the `Figure` class instance `fig`.

Too much theory? Try it out yourself below.



```python
fig = plt.figure()

x = np.arange(0,5,0.1)
y = np.sin(x)

# main axes
axes1 = fig.add_axes([0.1, 0.1, 0.9, 0.9])  # left, bottom, width, height (range 0 to 1)

# inner axes
axes2 = fig.add_axes([0.2, 0.2, 0.4, 0.4])

# main figure
axes1.plot(x, y, 'r') # 'r' = red line
axes1.set_xlabel('x')
axes1.set_ylabel('y')
axes1.set_title('Sine Wave')

# inner figure
x2 = np.arange(-5,5,0.1)
y2 = x2 ** 2
axes2.plot(x2,y2, 'g')   # 'g' = green line
axes2.set_xlabel('x2')
axes2.set_ylabel('y2')
axes2.set_title('Square Wave')

plt.show()
```


![png](/assets/images/MatplotlibExplained/output_22_0.png)


If you don't care about the specific location of second graph, try:


```python
fig, axes = plt.subplots(nrows=1, ncols=3)

x = np.arange(-5,5,0.1)
y = x**2
i=1
for ax in axes:
    ax.plot(x, y, 'r')
    ax.set_xlabel('x')
    ax.set_ylabel('y')
    ax.set_title('Square Wave '+str(i))
    i+=1
```


![png](/assets/images/MatplotlibExplained/output_24_0.png)


That was easy, but it isn't so pretty with overlapping figure axes and labels, right?

We can deal with that by using the `fig.tight_layout` method, which automatically adjusts the positions of the axes on the figure canvas so that there is no overlapping content. Moreover, the size of figure is fixed by default, i.e. it does not change depending on the subplots amount on the figure.


```python
fig, axes = plt.subplots(nrows=1, ncols=3)

x = np.arange(0,5,0.1)
y = x**2
i=1
for ax in axes:
    ax.plot(x, y**(i+1), 'r')
    ax.set_xlabel('x')
    ax.set_ylabel('y')
    ax.set_title('Wave '+str(i))
    i+=1
fig.tight_layout()
```


![png](/assets/images/MatplotlibExplained/output_26_0.png)


Above set of plots can be obtained also using `add_subplot` method of `figure` object.


```python
fig = plt.figure()

for i in range(1,4):
    ax = fig.add_subplot(1, 3, i)   # (rows amount, columns amount, subplot number)
    ax.plot(x, y**(i+1), 'r')
    ax.set_xlabel('x')
    ax.set_ylabel('y')
    ax.set_title('Wave '+str(i))
    # clear x and y ticks
    # ax.set_xticks([])
    # ax.set_yticks([])
fig.tight_layout()
plt.show()
```


![png](/assets/images/MatplotlibExplained/output_28_0.png)



```python
ncols, nrows = 3, 3

fig, axes = plt.subplots(nrows, ncols)

for m in range(nrows):
    for n in range(ncols):
        axes[m, n].set_xticks([])
        axes[m, n].set_yticks([])
        axes[m, n].text(0.5, 0.5, "axes[{}, {}]".format(m, n),
                        horizontalalignment='center')
```


![png](/assets/images/MatplotlibExplained/output_29_0.png)


`subplot2grid` is a helper function that is similar to `plt.subplot` but uses 0-based indexing and let subplot to occupy multiple cells. Let's to see how it works.


```python
fig = plt.figure()

# Let's remove all labels  on the axes
def clear_ticklabels(ax):
    ax.set_yticklabels([])
    ax.set_xticklabels([])

ax0 = plt.subplot2grid((3, 3), (0, 0))
ax1 = plt.subplot2grid((3, 3), (0, 1))
ax2 = plt.subplot2grid((3, 3), (1, 0), colspan=2)
ax3 = plt.subplot2grid((3, 3), (2, 0), colspan=3)
ax4 = plt.subplot2grid((3, 3), (0, 2), rowspan=2)

axes = (ax0, ax1, ax2, ax3, ax4)
# Add all sublots
[ax.text(0.5, 0.5, "ax{}".format(n), horizontalalignment='center') for n, ax in enumerate(axes)]
# Cleare labels on axes
[clear_ticklabels(ax) for ax in axes]
plt.show()
```


![png](/assets/images/MatplotlibExplained/output_31_0.png)


### Figure size, aspect ratio and DPI

Matplotlib allows the aspect ratio, DPI and figure size to be specified when the `Figure` object is created, using the `figsize` and `dpi` keyword arguments. `figsize` is a tuple of the width and height of the figure in inches, and `dpi` is the dots-per-inch (pixel per inch). To create an 800x400 pixel, 100 dots-per-inch figure, we can do:


```python
fig = plt.figure(figsize=(8,4), dpi=100)
```


    <Figure size 800x400 with 0 Axes>



```python
fig, axes = plt.subplots(figsize=(12,3))

axes.plot(x, y, 'r')
axes.set_xlabel('x')
axes.set_ylabel('y')
axes.set_title('title')
```




![png](/assets/images/MatplotlibExplained/output_35_1.png)
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
