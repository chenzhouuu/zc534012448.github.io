---
title: Introduction to Numpy
layout: post
date: 2019-01-19 11:20
image: /assets/images/NumpyExplained/numpy.jpeg
headerImage: true
tag:
- numpy
- tutorial
- Explained

star: false
category: blog
author: Rohit Midha
---
This is the second tutorial of the Explained! series.

I will be cataloging all the work I do with regards to PyLibraries and will share it here or on [my Github](http://bit.ly/RohitMidha23GitHub).

I will also be updating this post as and when I work on Numpy.

That being said, Dive in!



## Numpy

NumPy is the fundamental package for scientific computing with Python.

In Python, data is almost universally represented as NumPy arrays. Even newer tools like Pandas are built around the NumPy array.

We will be seeing:
1. 1D array, 2D array
2. Array slices, joins, subsets
3. Arithmetic Operations on 2D arrays
4. Covariance, Correlation  


### Initializing Numpy Arrays


1. Using np.array
2. Using np.ndarray


```python
import numpy as np
np.random.seed(0)  # seed for reproducibility
x1 = np.random.randint(10, size=6)  # One-dimensional array
x2 = np.random.randint(10, size=(3, 3))  # Two-dimensional array
```


```python
print(x1)
```

    [5 0 3 3 7 9]



```python
print(x2)
```

    [[3 5 2]
     [4 7 6]
     [8 8 1]]


# Using np.array()



```python
x1 = np.array([1,2,3,4])
print(x1)
print(type(x1))
```

    [1 2 3 4]
    <class 'numpy.ndarray'>



```python
x2 = np.array([[1,2,3],[4,5,6]])
print(x2)
print(type(x2))
```

    [[1 2 3]
     [4 5 6]]
    <class 'numpy.ndarray'>


## Using np.ndarray()


```python
x = np.ndarray(shape=3,dtype=int, buffer = np.array([1,2,3]))
print(x)
x = np.append(x,5)
print(x)
print(type(x))
```

    [1 2 3]
    [1 2 3 5]
    <class 'numpy.ndarray'>



```python
x = np.ndarray(shape=(2,2), dtype=float,buffer = np.array([[1.4,2.5],[1.3,2.4]]))
print(x)
```

    [[1.4 2.5]
     [1.3 2.4]]



```python
x = np.ndarray(shape=(2,2), dtype=int,buffer = np.array([[1,2],[1,2]]))
print(x)
```

    [[1 2]
     [1 2]]


## Attributes of ndarray

Each array has attributes `ndim` (the number of dimensions), `shape` (the size of each dimension), and `size` (the total size of the array):


```python
x2 = np.array([[1,2,3],[4,5,6]])
print("x2.ndim = ",x2.ndim)
print("x2.shape = ",x2.shape)
print("x2.size = ",x2.size)
```

    x2.ndim =  2
    x2.shape =  (2, 3)
    x2.size =  6


Another useful attribute is the `dtype` which tells you about the type of elements in the array:


```python
print("x2.dtype = ",x2.dtype)
```

    x2.dtype =  int64


Other attributes include `itemsize`, which lists the size (in bytes) of each array element, and `nbytes`, which lists the total size (in bytes) of the array:


```python
print("itemsize:", x.itemsize, "bytes")
print("nbytes:", x2.nbytes, "bytes")
```

    itemsize: 8 bytes
    nbytes: 48 bytes



## Array Indexing: Accessing Single Elements

In a one-dimensional array, the ith value (counting from zero) can be accessed by specifying the desired index in square brackets, just as with Python lists:


```python
x1 = np.array([1,2,3,4])
print("x1 = ",x1)
print("x1[0] = ",x1[0]) # just like arrays in c/c++
print("x1[-1] = ",x1[-1]) # negative indexing just like lists
```

    x1 =  [1 2 3 4]
    x1[0] =  1
    x1[-1] =  4


In a multi-dimensional array, items can be accessed using a comma-separated tuple of indices:


```python
x2 = np.array([[1,2,3],[4,5,6],[7,8,9]])
print("x2 = "); print(x2)
print("x2[0] = ",x2[0]) # will print the entire 1st row

# to print 1st element of 1st row
print("x2[0][0]= ", x2[0][0])
print("x2[0,0] = ",x2[0,0])

# to print 2nd element of 3rd row
print("x2[2][1]= ", x2[2][1])
print("x2[2,1]= ", x2[2,1])

```

    x2 =
    [[1 2 3]
     [4 5 6]
     [7 8 9]]
    x2[0] =  [1 2 3]
    x2[0][0]=  1
    x2[0,0] =  1
    x2[2][1]=  8
    x2[2,1]=  8


Values can also be modified using any of the above index notation:


```python
x2[0, 0] = 12
print(x2)
```

    [[12  2  3]
     [ 4  5  6]
     [ 7  8  9]]



```python
x2[0][0] = 14
print(x2)
```

    [[14  2  3]
     [ 4  5  6]
     [ 7  8  9]]


**NOTE :** Unlike Python lists, NumPy arrays have a fixed type. This means, for example, if you attempt to insert a floating-point value to an integer array, the value will be silently truncated.

i.e the float value gets converted to nearest int value.


```python
x1 = np.ndarray(5, buffer = np.array([1,2,3,4,5]),dtype = int)
print(x1)
x1[2] = 5.7
print("x1 after changing : ",x1)
```

    [1 2 3 4 5]
    x1 after changing :  [1 2 5 4 5]

## Array Slicing and Subsetting : Accessing Subarrays

Just as we can use square brackets to access individual array elements, we can also use them to access subarrays with the slice notation, marked by the colon (:) character. The NumPy slicing syntax follows that of the standard Python list; to access a slice of an array x, use :
```python
x[start:stop:step]
```
**NOTE :** Default value of `start` is `0`, `stop` is `size of object` and `step` is `1`.


```python
x = np.ndarray(10, buffer = np.array([0,1,2,3,4,5,6,7,8,9]),dtype = int)
print(x)
print("x[:] = ",x[:])
print("x[:5] = ",x[:5])
print("x[5:] = ",x[5:])
print("x[1:5] = ",x[1:5])
print("x[1:5:2] = ",x[1:5:2])
print("x[::-1] = ",x[::-1])
```

    [0 1 2 3 4 5 6 7 8 9]
    x[:] =  [0 1 2 3 4 5 6 7 8 9]
    x[:5] =  [0 1 2 3 4]
    x[5:] =  [5 6 7 8 9]
    x[1:5] =  [1 2 3 4]
    x[1:5:2] =  [1 3]
    x[::-1] =  [9 8 7 6 5 4 3 2 1 0]



```python
np.random.seed(0)  # seed for reproducibility
x2 = np.array([[1,2,3],[4,5,6],[7,8,9]])
print(x2)
print("x2[:2, :3] = "); print(x2[:2, :3])  # first two rows, first three columns
print("x2[:3, ::2] = "); print(x2[:3, ::2]) # all rows, every other column
print("x2[::-1, ::-1] = "); print(x2[::-1, ::-1]) #reversed 2D array
print("x2[:, 0] = ",x2[:, 0])  # first column of x2
```

    [[1 2 3]
     [4 5 6]
     [7 8 9]]
    x2[:2, :3] =
    [[1 2 3]
     [4 5 6]]
    x2[:3, ::2] =
    [[1 3]
     [4 6]
     [7 9]]
    x2[::-1, ::-1] =
    [[9 8 7]
     [6 5 4]
     [3 2 1]]
    x2[:, 0] =  [1 4 7]

## Joining Two Arrays

Joining of two arrays in NumPy, is primarily accomplished using the routine `np.concatenate`.


```python
x = np.array([1,2,3])
y = np.array([4,5,6])
z = np.concatenate([x,y]) # Combines x and y to give one array.
# a = np.concatenate([x,y,z])
print(z)
# print(a)
```

    [1 2 3 4 5 6]



```python
x2 = np.array([[1,2,3],[2,3,4]])
y2 = np.array([[3,4,5],[4,5,6]])
z2 = np.concatenate([x2,y2])
print(z2)
```

    [[1 2 3]
     [2 3 4]
     [3 4 5]
     [4 5 6]]


# Arithmetic Operations on 2D arrays

| Operator 	| Equivalent Function 	|
|----------	|---------------------	|
| +        	| np.add              	|
| -        	| np.subtract         	|
| *        	| np.multiply         	|


```python
x2 = np.array([[1,2,3],[2,3,4]])
y2 = np.array([[3,4,5],[4,5,6]])
print("x2 + y2 = "); print(np.add(x2,y2))
print("x2 - y2 = "); print(np.subtract(x2,y2))
```

    x2 + y2 =
    [[ 4  6  8]
     [ 6  8 10]]
    x2 - y2 =
    [[-2 -2 -2]
     [-2 -2 -2]]



```python
print(x2)
print(y2)
print("x2 * y2 = "); print(np.multiply(x2,y2))
```

    [[1 2 3]
     [2 3 4]]
    [[3 4 5]
     [4 5 6]]
    x2 * y2 =
    [[ 3  8 15]
     [ 8 15 24]]


**NOTE :** Here as you can see, matrix multiplication isn't actually possible and we actually just get a matrix where `x2[i,j] * y2[1,j]` is the output.


```python
x2 = np.array([[1,2,3],[2,3,4]])
y2 = np.array([[3,4,5],[4,5,6]])
print(np.matmul(x2,y2))
# This gives an error. Why?
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-28-389e99023c8e> in <module>
          1 x2 = np.array([[1,2,3],[2,3,4]])
          2 y2 = np.array([[3,4,5],[4,5,6]])
    ----> 3 print(np.matmul(x2,y2))
          4 # This gives an error. Why?


    ValueError: shapes (2,3) and (2,3) not aligned: 3 (dim 1) != 2 (dim 0)



```python
x2 = np.array([[1,2,3],[2,3,4]])
y2 = np.array([[3,4],[4,5],[5,6]])
print(np.matmul(x2,y2))
```

    [[26 32]
     [38 47]]


## Covariance

Covariance indicates the level to which two variables vary together.

If we examine N-dimensional samples, `X = [x_1, x_2, ... x_N]^T`, then the covariance matrix element `C_{ij}` is the covariance of `x_i` and `x_j`. The element `C_{ii}` is the variance of `x_i`.


```python
x2 = np.array([[0,1,2],[2,1,0]])
print(x2)
```

    [[0 1 2]
     [2 1 0]]


Note here how `x[0]` increases and `x[1]` decreases.

This is also shown by the covariance matrix :


```python
print(np.cov(x2))
```

    [[ 1. -1.]
     [-1.  1.]]


Note that again, `C[0,1]` and `C[1,0]` which shows the correlation between `x[0]` and `x[1]`, is negative.

However `C[0,0]` and `C[1,1]` which show the correlation between `x[0]` and `x[0]` and `x[1]` and `x[1]` is 1.


Note how x and y are combined:


```python
x = np.array([-2.1, -1,  4.3])
y = np.array([3,  1.1,  0.12])
X = np.stack((x, y))
print(np.cov(X))
# To check
print(np.cov(x))
print(np.cov(y))
```

    [[11.71       -4.286     ]
     [-4.286       2.14413333]]
    11.709999999999999
    2.1441333333333334

# Correlation

The term "correlation" refers to a mutual relationship or association between quantities.
It is a standardised form of Covariance.

Correlation Coeffecients take values between `[-1,1]`

In Numpy (and in general), Correlation Matrix refers to the normalised version of a Covariance matrix.


```python
x = np.array([-2.1, -1,  4.3])
y = np.array([3,  1.1,  0.12])
X = np.stack((x, y))
print(np.corrcoef(X))
```

    [[ 1.         -0.85535781]
     [-0.85535781  1.        ]]

---

<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/RohitMidha23" data-size="large" data-show-count="true" aria-label="Follow @RohitMidha23 on GitHub">Follow @RohitMidha23</a>
<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>

Find more at my Github repository [Explained](http://bit.ly/ExplainedRepo).

Show some :heart: by :star:ing it.

<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/RohitMidha23/Explained" data-size="large" data-show-count="true" aria-label="Star RohitMidha23/Explained on GitHub">Star</a>
<a href="https://github.com/RohitMidha23/Explained" class="github-corner" aria-label="View source on GitHub"><svg width="80" height="80" viewBox="0 0 250 250" style="fill:#fff; color:#151513; position: absolute; top: 0; border: 0; left: 0; transform: scale(-1, 1);" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" style="transform-origin: 130px 106px;" class="octo-arm"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor" class="octo-body"></path></svg></a><style>.github-corner:hover .octo-arm{animation:octocat-wave 560ms ease-in-out}@keyframes octocat-wave{0%,100%{transform:rotate(0)}20%,60%{transform:rotate(-25deg)}40%,80%{transform:rotate(10deg)}}@media (max-width:500px){.github-corner:hover .octo-arm{animation:none}.github-corner .octo-arm{animation:octocat-wave 560ms ease-in-out}}</style>
