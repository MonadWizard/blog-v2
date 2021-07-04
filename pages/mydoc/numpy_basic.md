---
title: numpy basic
keywords: numpy  Bangla Tutorials, bangla numpy, Bangla Python, Blog Bangla, Monad wizard
last_updated: Aug 04 , 2020
# tags: [getting_started]
summary: 'Here I try to complete all Basic Numpy Topic with short note. '
sidebar: mydoc_sidebar
permalink: numpy_basic.html
folder: mydoc
---

numpy কে numerical python মনে করা যায়। python এ array নিয়ে কাজ করার জন্য এবং লিনিয়ার বীজগণিত, ফুরিয়ার ট্রান্সফর্ম এবং ম্যাট্রিকেসের ডোমেনে কাজ করার জন্য numpy বহল প্রচলিত।

Basic usefull কিছু function এবং example এর দ্বারা numpy এর syntax এবং demo দেখানো হল।

### 1d array

numpy এ array define করতে just <font color="green"> np.array([], np.data_type) </font> ব্যবহার করলেই চলবে। [সকল numpy data-type দেখতে](https://numpy.org/doc/stable/user/basics.types.html)

<font color="red"> Example </font>

```python
import numpy as np

x = np.array([1, 2, 3], np.int16)

print(x)
print(type(x))

print(x[0]); print(x[1]); print(x[2]); print(x[-1])  # -1 print last index
#print(x[-1]); print(x[3]) # out of range cause list index start from 0

```

<font color="red"> Output : </font>

    [1 2 3]
    <class 'numpy.ndarray'>
    1
    2
    3
    3

### 2d array

আমরা numpy এ one dimention বা multi-dimention array নিয়ে কাজ করার জন্য <font color="green"> np.array([], np.data_type) </font> এর array([],[],[]) এই রূপে define করে কাজ করা যায়।

<font color="red"> Example </font>

```python
import numpy as np
x = np.array([[1, 2, 3], [4, 5, 6]], np.int16)
print(x)
print(x[0, 0]); print(x[0, 1]); print(x[0, 2])
print(x[:, 0])
print(x[:, 1])
print(x[:, 2])
print(x[0, :])
print(x[1, :])
```

<font color="red"> Output : </font>

    [[1 2 3]
     [4 5 6]]
    1
    2
    3
    [1 4]
    [2 5]
    [3 6]
    [1 2 3]
    [4 5 6]

### 3d array

2d array এর same structure এ define করা যায়।

<font color="red"> Example </font>

```python
import numpy as np
x = np.array([[[1, 2, 3], [4, 5, 6]],[[0, -1, -2], [-3, -4, -5]]], np.int16)
print(x)
print(x [0, 0, 0])
print(x [1, 1, 2])
print(x[:, 1, 1])
```

<font color="red"> Output : </font>

    [[[ 1  2  3]
      [ 4  5  6]]

     [[ 0 -1 -2]
      [-3 -4 -5]]]
    1
    -5
    [ 5 -4]

### NumPy Ndarray Properties

2d or 3d array structure এর মতই ।

<font color="red"> Example </font>

```python
import numpy as np
x = np.array([[[1, 2, 3], [4, 5, 6]],[[0, -1, -2], [-3, -4, -5]]], np.int16)
print(x)
print(x.shape)
print(x.ndim)
print(x.dtype)

print(x.size)
print(x.nbytes)
print(x.T)
```

<font color="red"> Output : </font>

    [[[ 1  2  3]
      [ 4  5  6]]

     [[ 0 -1 -2]
      [-3 -4 -5]]]
    (2, 2, 3)
    3
    int16
    12
    24
    [[[ 1  0]
      [ 4 -3]]

     [[ 2 -1]
      [ 5 -4]]

     [[ 3 -2]
      [ 6 -5]]]

### NumPy Constants

numpy এ বেশ কিছু constant number নিয়ে mathmathical calculation করা হয়।

data-set এর error-collection বা বিভিন্ন mathmathical soluation এর জন্য numpy ব্যবহার করে খুব সহজে এই সব constant ব্যবহার করা যায়।

-   possitive infinity number নিয়ে কাজ করতে হয় তবে <mark>np.inf </mark> define করলেই হবে।
-   Euler's Constant number নিয়ে কাজ করতে হয় তবে <mark>np.e </mark> define করলেই হবে।
-   Not A Number নিয়ে কাজ করতে হয় তবে <mark>np.NAN </mark> define করলেই হবে।
-   pi value নিয়ে কাজ করতে হয় তবে <mark>np.pi </mark> define করলেই হবে।

একই ভাবে অন্য সব Constant example এ দেখানো হল।

[official doc এ সকল constant দেখতে](https://numpy.org/doc/stable/reference/constants.html)

<font color="red"> Example : </font>

```python
print(np.inf) # representation of "infinity" or possitive infinity
print(np.NAN) # representation of "Not A Number"
print(np.NINF) # representation of "negative infinity"
print(np.NZERO) # representation of "negative Zero"
print(np.PZERO) # representation of "possitive Zero"

# scientific Constants
print(np.e) # representation of "Euler’s constant"
print(np.euler_gamma)  # representation of "Euler’s gamma "
print(np.pi) # representation of "Pi"
```

<font color="red"> Output : </font>

    inf
    nan
    -inf
    -0.0
    0.0
    2.718281828459045
    0.5772156649015329
    3.141592653589793

## Martix

### .empty()

<font color="green"> np.empty([rows, columns], np.dataType) </font> define করে random value এর matrix তৈরি করতে পারি। random value এর মানগুলো করে datatype এর length এর মদ্ধেকার যে কোন মান হয়।

<font color="red"> example </font>

```python
import numpy as np

x = np.empty([4, 3], np.uint8)
print(x)
```

<font color="red"> Output : </font>

    [[0 0 0]
     [0 0 0]
     [0 0 0]
     [0 0 0]]

### .eye()

<font color="green"> np.eye(rows, columns, np.dataType, diagonal) </font> define করতে হয়। কিন্তু columns এবং diagonal এর মান optional.

<font color="red"> Example : </font>

```python
import numpy as np

y = np.eye(5, dtype=np.uint8)
z = np.eye(5,4,dtype=np.uint8)
print(y)
print("\n")
print(z)

```

<font color="red"> Output : </font>

    [[1 0 0 0 0]
     [0 1 0 0 0]
     [0 0 1 0 0]
     [0 0 0 1 0]
     [0 0 0 0 1]]


    [[1 0 0 0]
     [0 1 0 0]
     [0 0 1 0]
     [0 0 0 1]
     [0 0 0 0]]

<mark> change diagonal value </mark>

k = diagonal এর মান, যা 1 ব্যবহার করে ১ diagonal সামনে নিতে পারা যায় ।

```python
import numpy as np

y = np.eye(5, dtype=np.uint8, k=1)
print(y)
```

<font color="red"> Output : </font>

    [[0 1 0 0 0]
     [0 0 1 0 0]
     [0 0 0 1 0]
     [0 0 0 0 1]
     [0 0 0 0 0]]

k = diagonal এর মান, যা -1 ব্যবহার করে o থেকে ১ diagonal পেছনে নিতে পারা যায় ।

```python
import numpy as np

y = np.eye(5, dtype=np.uint8, k=-1)
print(y)
```

<font color="red"> Output : </font>

    [[0 0 0 0 0]
     [1 0 0 0 0]
     [0 1 0 0 0]
     [0 0 1 0 0]
     [0 0 0 1 0]]

### identity matrix

<font color="green"> np.identity(value, np.dataType) </font> ব্যবহার করে identity matrix তৈরি করা যায়।

<font color="red"> Example : </font>

```python
import numpy as np

x = np.identity(5, dtype= np.uint8)
print(x)
```

<font color="red"> Output : </font>

    [[1 0 0 0 0]
     [0 1 0 0 0]
     [0 0 1 0 0]
     [0 0 0 1 0]
     [0 0 0 0 1]]

### ones matrix

numpy এ একই সঙ্ঘে multi dimentional matrix তৈরি করা যায়।
<font color="green"> np.ones(shape=(dimention,rows,columns), dtype=np.dataType) </font>

<font color="red"> Example : </font>

```python
import numpy as np
x = np.ones((2, 4, 5,), dtype=np.int16) # 3d
y = np.ones(shape=(2,4,3,2), dtype=np.int16) # 4d
print(x)
#print(y)
```

<font color="red"> Output : </font>

    [[[1 1 1 1 1]
      [1 1 1 1 1]
      [1 1 1 1 1]
      [1 1 1 1 1]]

     [[1 1 1 1 1]
      [1 1 1 1 1]
      [1 1 1 1 1]
      [1 1 1 1 1]]]

### zeroes matrix

zeros matrix আর ones matrix তৈরি করার উপায় same.
<font color="green"> np.zeros(shape=(dimention,rows,columns), dtype=np.dataType) </font>

<font color="red"> Example : </font>

```python
import numpy as np

y = np.zeros((2, 4, 5), dtype=np.int16) #3d
x = np.zeros((2, 3, 3, 2), dtype=np.int16) #4d
print(x)
#print(y)
```

<font color="red"> Output : </font>

    [[[[0 0]
       [0 0]
       [0 0]]

      [[0 0]
       [0 0]
       [0 0]]

      [[0 0]
       [0 0]
       [0 0]]]


     [[[0 0]
       [0 0]
       [0 0]]

      [[0 0]
       [0 0]
       [0 0]]

      [[0 0]
       [0 0]
       [0 0]]]]

### .full()

.full method ব্যবহার করে multi-dimentional matrix প্রয়োজনীয় value দ্বারা পূর্ণ করে তৈরি করা যায়।
<font color="green"> np.full(shape=(dimention,rows,columns), dtype=np.dataType, fill_value) </font>
fill_value parameter এ আমরা যে data বা specific list define করব full matrix টি সেই data দ্বারা তৈরি হবে। অন্য সব parameter same।

<font color="red"> Example : </font>

```python
import numpy as np

x = np.full((3, 3, 3), dtype=np.int16, fill_value = 5)
y = np.full(shape=(2, 2), dtype=np.int16, fill_value = [4,9])

print(x)
print("\n")
print(y)
```

<font color="red"> Output : </font>

    [[[5 5 5]
      [5 5 5]
      [5 5 5]]

     [[5 5 5]
      [5 5 5]
      [5 5 5]]

     [[5 5 5]
      [5 5 5]
      [5 5 5]]]


    [[4 9]
     [4 9]]

## Matrix creation routines

### .tri()

lower triangular matix বানাইতে .tri() ব্যবহার করা হয়। .tri() দ্বারা তৈরি করা matrix এর diagonal value গুলো 1 হয় এবং diagonal এর uper-triangular part 0 এবং lower-triangular part 1 দ্বারা তৈরি হয়।

<font color="green"> np.tri(N=rows, M=columns, k=diagonal, dtype=np.dataType) </font>

<font color="red"> Example : </font>

```python
import numpy as np

x = np.tri(3, 3, k=0, dtype=np.uint16)
print(x)
```

<font color="red"> Output : </font>

    [[1 0 0]
     [1 1 0]
     [1 1 1]]

k= diagonal value পরিবর্তন করে triangular shape পরিবর্তন করা যায়।

```python
import numpy as np

x = np.tri(5, 5, k=1, dtype=np.uint16)
print(x)
```

<font color="red"> Output : </font>

    [[1 1 0 0 0]
     [1 1 1 0 0]
     [1 1 1 1 0]
     [1 1 1 1 1]
     [1 1 1 1 1]]

```python
import numpy as np

x = np.tri(5, k=-1, dtype=np.uint16)
print(x)
```

<font color="red"> Output : </font>

    [[0 0 0 0 0]
     [1 0 0 0 0]
     [1 1 0 0 0]
     [1 1 1 0 0]
     [1 1 1 1 0]]

### tril() and triu()

যে কোন matrix থেকে triangular matrix বানানোর জন্য tril() বা triu() ব্যবহার করা হয়।

-   tril() ব্যবহার করলে diagonal value থেকে lower triangle value গুলো অপরিবর্তিত থেকে uper triangle 0 দ্বারা তৈরি হয়।
-   triu() ব্যবহার করলে diagonal value থেকে upper triangle value গুলো অপরিবর্তিত থেকে lower triangle 0 দ্বারা তৈরি হয়।

<font color="green"> np.tril(matrix, k=diagonal) </font> or same as <font color="green"> np.triu(2d_array, k=diagonal) </font>

<font color="red"> Example : </font>

```python
import numpy as np
x = np.ones((5, 5), dtype=np.uint8)
y1 = np.tril(x, k=1)
y2 = np.triu(x, k=-1)

print(x)
print("\n")
print(y1)
print("\n")
print(y2)
```

<font color="red"> Output : </font>

    [[1 1 1 1 1]
     [1 1 1 1 1]
     [1 1 1 1 1]
     [1 1 1 1 1]
     [1 1 1 1 1]]


    [[1 1 0 0 0]
     [1 1 1 0 0]
     [1 1 1 1 0]
     [1 1 1 1 1]
     [1 1 1 1 1]]


    [[1 1 1 1 1]
     [1 1 1 1 1]
     [0 1 1 1 1]
     [0 0 1 1 1]
     [0 0 0 1 1]]

## random methods

### random.randint()

numpy এর random method ব্যবহার করে অনেক type এর random value তৈরি করা যায়। <mark> randint() </mark> random method এর একটা sub-method যা ব্যবহার করে যে কোন range এবং যে কোন length এর integer সংখ্যার random value তৈরি করা যায়।

<font color="green"> np.random.randint( low, high, size) </font>

-   low এ minimum range value
-   high এ maximum range value
-   size এ total length

<font color="red"> Example : </font>

```python
import numpy as np
x = np.random.randint( low = 0, high = 9, size = 10)
print(type(x))
print("x", x, "\n\n")

x1 = np.random.randint(6, size=10)  # maximum random intiger value < 6

# Generate a 2 x 4 array of ints between 0 and 4, inclusive:
x2 = np.random.randint(5, size=(2, 4))

# Generate a 1 x 3 array with 3 different upper bounds
x3 = np.random.randint(1, [3, 5, 10])

# Generate a 1 by 3 array with 3 different lower bounds
x4 = np.random.randint([1, 5, 7], 10)

# Generate a 2 by 4 array using broadcasting with dtype of uint8
x6 = np.random.randint([1, 3, 5, 7], [[10], [20]], dtype=np.uint8)

print("x1", x1, "\n"); print("x2", x2, "\n"); print("x3",x3, "\n"); print("x4", x4, "\n");
print("x6",x6, "\n");
```

<font color="red"> Output : </font>

    <class 'numpy.ndarray'>
    x [1 6 3 0 0 0 1 5 2 7]


    x1 [3 5 1 4 3 4 4 0 1 3]

    x2 [[4 2 0 0]
     [4 4 2 3]]

    x3 [1 4 8]

    x4 [7 9 9]

    x6 [[ 7  7  8  8]
     [ 4  5 10 15]]

### random.rand()

0 থেকে 1 এর মধ্যে uniform distribution number তৈরি করার জন্য <mark> rand() </mark> method ব্যবহার করা হয়।

<font color="green"> np.random.rand( rows, columns) </font>

rand() এ শুধ dimention বা row,column define করলেই হয়।

<font color="red"> Example : </font>

```python
import numpy as np

x = np.random.rand(3, 4)
print(x)
print(type(x))
```

<font color="red"> Output : </font>

    [[0.40006156 0.1669452  0.96511364 0.01640715]
     [0.19352619 0.81856315 0.82489604 0.93155834]
     [0.25856532 0.90158158 0.57748178 0.41655122]]
    <class 'numpy.ndarray'>

```python
import numpy as np

x = np.random.rand(2, 3, 4)
print(x)
```

<font color="red"> Output : </font>

    [[[0.97850534 0.58589313 0.50242842 0.93059539]
      [0.30056528 0.81815384 0.91870242 0.92486857]
      [0.69421277 0.71896174 0.79699254 0.07864825]]

     [[0.81464694 0.58391654 0.37930517 0.72814581]
      [0.02619663 0.81431023 0.54525695 0.11930859]
      [0.74915898 0.77662649 0.88700412 0.94952753]]]

## Array Manipulation Routines

### .arange()

python এর range function এর মতই numpy এর arange function.

<font color="green"> np.arange( start, stop, step) </font>

<font color="red"> Example : </font>

```python
import numpy as np
x = np.arange(6)
x1 = np.arange(2,6)
x2 = np.arange(0,10,3)

print(x); print(x1); print(x2);

```

<font color="red"> Output : </font>

    [0 1 2 3 4 5]
    [2 3 4 5]
    [0 3 6 9]

### .reshape()

array এর dimention change করতে reshape ব্যবহার করা হয়। যে কোন array এর structure কে সঠিক অনুপাতে পরিবর্তন করতে <font color="green"> array.reshape((row,column),order) </font>
or <font color="green"> numpy.reshape(old_array,newshape,order) </font>
ব্যবহার করা যায়।

<font color="red"> Example : </font>

```python
import numpy as np
x = np.arange(6)
y = x.reshape((3, 2))
print(y, "\n\n")

x1 = np.reshape(x, 6)
print(x1)
```

<font color="red"> Output : </font>

    [[0 1]
     [2 3]
     [4 5]]


    [0 1 2 3 4 5]

### .array()

.array() ব্যবহার করে যে কোন data-type এর যে কোন যে কোন dimention এর array বানাইতে পারা যায়।

<font color="red"> Example : </font>

```python
import numpy as np
x = np.array([[0, 1, 2], [3, 4, 5]], dtype = np.uint8)
print(x)
print(x.dtype)
```

<font color="red"> Output : </font>

    [[0 1 2]
     [3 4 5]]
    uint8

### .flatten()

যে কোন dimention থেকে array কে one dimention এ পরিণত করার জন্য .flatten() method ব্যবহার করা হয়।

<font color="green"> anyDarray.flatten(order) </font>

<font color="red"> Example : </font>

```python
import numpy as np

x = np.array([[0, 1, 2], [3, 4, 5]], dtype = np.uint8)
y = x.flatten()
print(y)
```

<font color="red"> Output : </font>

    [0 1 2 3 4 5]

<mark> using order </mark>

-   C flatten in row major. (default)
-   F flatten in column major
-   A flatten same as F in Fortran contiguous else flatten as C
-   K flatten ordered in memory

```python
import numpy as np

x = np.array([[0, 1, 2], [3, 4, 5]], dtype = np.uint8)
print(x,  '\n\n')

y = x.flatten('C')
print(y, '\n\n')

y = x.flatten('F')
print(y)
```

<font color="red"> Output : </font>

    [[0 1 2]
     [3 4 5]]


    [0 1 2 3 4 5]


    [0 3 1 4 2 5]

### .ravel()

ravel() ও 1-dimentional array বানাইতে ব্যবহার করা হয়। just syntax একটু আলাদা।

<font color="green"> numpy.ravel(anyDarray, order) </font>

ravel function এর order গুলো flatten method এর অনুরূপ।

<font color="red"> Example : </font>

```python
import numpy as np

x = np.array([[0, 1, 2], [3, 4, 5]], dtype = np.uint8)
y = np.ravel(x)
print(y,"\n")
print(x)
```

<font color="red"> Output : </font>

    [0 1 2 3 4 5]

    [[0 1 2]
     [3 4 5]]

<Mark> axis = 0 means columns </mark>

<Mark> axis = 1 means rows </mark>

### .stack()

একাধিক array কে join করার জন্য stack function ব্যবহার করা হয়।

-   np.vstack: ব্যবহার করে vertical axis বরাবর join করা হয়।
-   np.hstack: ব্যবহার করে horizontal axis বরাবর join করা হয়।
-   np.column_stack: ব্যবহার করে 1-D array কে columns হিসেবে 2-D array তে join করা হয়।
-   np.row_stack: ব্যবহার করে 1-D array কে rows হিসেবে 2-D array তে join করা হয়।
-   np.concatenate: ব্যবহার করে array এর specified axis join করা হয়। (axis is passed as argument).

<font color="red"> Example : </font>

```python
import numpy as np


x = np.array([1, 2, 3], dtype = np.uint8)
y = np.array([4, 5, 6], dtype = np.uint8)

z = np.stack((x, y), axis = 0)
print("join them together: \n", z)
print("shape: \t", z.shape , "\n\n")

z = np.stack((x, y), axis = -1 )
print("axis= -1 \n",z)
print("shape: \t", z.shape , "\n\n")

z = np.stack((x, y), axis = 1 )
print("axis= 1 \n",z)
print("shape: \t", z.shape , "\n\n")

z = np.hstack((x, y))
print("hstack \n", z)
print("shape: \t", z.shape , "\n\n")

z = np.vstack((x, y))
print("vstack \n", z)
print("shape: \t", z.shape , "\n\n")

a = np.array([[1, 2],[3, 4]])
b = np.array([[5, 6],[7, 8]])
c = np.array([0,0])

z = np.column_stack((a,c))
print("column_stack \n", z)
print("shape: \t", z.shape , "\n\n")

z = np.row_stack((a,c))
print("row_stack \n", z)
print("shape: \t", z.shape , "\n\n")

z = np.concatenate((a,b), axis=1)
print("concatenate \n", z)
print("shape: \t", z.shape , "\n\n")
```

<font color="red"> Output : </font>

    join them together:
     [[1 2 3]
     [4 5 6]]
    shape:   (2, 3)


    axis= -1
     [[1 4]
     [2 5]
     [3 6]]
    shape:   (3, 2)


    axis= 1
     [[1 4]
     [2 5]
     [3 6]]
    shape:   (3, 2)


    hstack
     [1 2 3 4 5 6]
    shape:   (6,)


    vstack
     [[1 2 3]
     [4 5 6]]
    shape:   (2, 3)


    column_stack
     [[1 2 0]
     [3 4 0]]
    shape:   (2, 3)


    row_stack
     [[1 2]
     [3 4]
     [0 0]]
    shape:   (3, 2)


    concatenate
     [[1 2 5 6]
     [3 4 7 8]]
    shape:   (2, 4)

### .split()

array কে একাধিক segment এ ভাগ করার জন্য .split() ব্যবহার করা হয়।

<font color="green"> numpy.split(array,section,axis) </font>

-   np.hsplit: array কে horizontal axis বরাবর Split করে।
-   np.vsplit: array কে vertical axis বরাবর Split করে।
-   np.array_split: array কে specified axis বরাবর Split করে।
-   np.dsplit : depth এর উপর ভিত্তি করে array কে multiple sub-set এ split করে।

<font color="red"> Example : </font>

```python
import numpy as np

a = np.array([[1, 3, 5, 7, 9, 11],
              [2, 4, 6, 8, 10, 12]])

z = np.hsplit(a, 2)
print("hsplit : \n",z,"\n\n" )

z = np.vsplit(a,2)[1]
print("vsplit : \n",z,"\n\n" )

z = np.array_split(a, 2, axis=1)
print("harray_split : \n",z,"\n\n" )

```

<font color="red"> Output : </font>

    hsplit :
     [array([[1, 3, 5],
           [2, 4, 6]]), array([[ 7,  9, 11],
           [ 8, 10, 12]])]


    vsplit :
     [[ 2  4  6  8 10 12]]


    harray_split :
     [array([[1, 3, 5],
           [2, 4, 6]]), array([[ 7,  9, 11],
           [ 8, 10, 12]])]

### .flip()

.flip() method ব্যবহার করে array এর shape একই থাকে শুধু element গুলো reordered করা হয়।

-   axis = 0 means columns
-   axis = 1 means rows
-   fliplr (flip left to right) flip horizontally (same as axis=1)
-   flipud (flip up to down) flip vertically (same as axis=0)

<font color="red"> Example : </font>

```python
import numpy as np

x = np.arange(10)
print(x, "\n")
print(np.flip(x),"\n\n")

x = np.arange(16).reshape(4, 4)
print(x)

y = np.flip(x, axis = 0)
print("axis=0 \n", y, "\n\n")

y = np.flip(x, axis = 1)
print("axis=1 \n", y, "\n\n")

print("---------------------------------")

y = np.fliplr(x)   #Flip an array horizontally (axis=1)
print(x)
print("fliplr \n",y, "\n\n")

y = np.flipud(x)   # Flip an array vertically (axis=0)
print(x)
print("flipud \n",y, "\n\n")

```

<font color="red"> Output : </font>

    [0 1 2 3 4 5 6 7 8 9]

    [9 8 7 6 5 4 3 2 1 0]


    [[ 0  1  2  3]
     [ 4  5  6  7]
     [ 8  9 10 11]
     [12 13 14 15]]
    axis=0
     [[12 13 14 15]
     [ 8  9 10 11]
     [ 4  5  6  7]
     [ 0  1  2  3]]


    axis=1
     [[ 3  2  1  0]
     [ 7  6  5  4]
     [11 10  9  8]
     [15 14 13 12]]


    ---------------------------------
    [[ 0  1  2  3]
     [ 4  5  6  7]
     [ 8  9 10 11]
     [12 13 14 15]]
    fliplr
     [[ 3  2  1  0]
     [ 7  6  5  4]
     [11 10  9  8]
     [15 14 13 12]]


    [[ 0  1  2  3]
     [ 4  5  6  7]
     [ 8  9 10 11]
     [12 13 14 15]]
    flipud
     [[12 13 14 15]
     [ 8  9 10 11]
     [ 4  5  6  7]
     [ 0  1  2  3]]

### rot90()

array কে specific axis অনুজায়ে 90 ডিগ্রি rotate করার জন্য .rot90() ব্যবহার করা হয়।

<font color="green"> numpy.rot90(anyDarray, numberOfTimeRotate, axes) </font>

<font color="red"> Example : </font>

```python
import numpy as np

x = np.arange(16).reshape(4, 4)
print(x, "\n\n")

y = np.rot90(x)
print(y)
```

<font color="red"> Output : </font>

    [[ 0  1  2  3]
     [ 4  5  6  7]
     [ 8  9 10 11]
     [12 13 14 15]]


    [[ 3  7 11 15]
     [ 2  6 10 14]
     [ 1  5  9 13]
     [ 0  4  8 12]]

### .roll()

shift element (0,0)index এ বসে তারপর থেকে বাকি সব index এর element গুলো synchronously change হয় ।

<font color="green"> numpy.roll(a, shift, axis=None) </font>

<font color="red"> Example : </font>

```python
import numpy as np

x = np.arange(16).reshape(4, 4)
print(x, "\n\n")

y = np.roll(x, shift=8)
print(y)


```

<font color="red"> Output : </font>

    [[ 0  1  2  3]
     [ 4  5  6  7]
     [ 8  9 10 11]
     [12 13 14 15]]


    [[ 8  9 10 11]
     [12 13 14 15]
     [ 0  1  2  3]
     [ 4  5  6  7]]

### bitwise operators

numpy এ multiple array এর মধ্যে bitwise operation করা হয়।

-   .bitwise_and(array1, array2)
-   .bitwise_or(array1, array2)
-   .bitwise_xor(array1, array2)
-   .bitwise_not(array1, array2)

<font color="red"> Example : </font>

```python
import numpy as np
x = np.array([0, 1, 0, 1], np.uint8)
y = np.array([0, 0, 1, 1], np.uint8)

print("and : \n",np.bitwise_and(x, y),"\n")
print("or : \n",np.bitwise_or(x, y),"\n")
print("xor : \n",np.bitwise_xor(x, y),"\n")
print("not : \n",np.bitwise_not(x),"\n")
```

<font color="red"> Output : </font>

    and :
     [0 0 0 1]

    or :
     [0 1 1 1]

    xor :
     [0 1 1 0]

    not :
     [255 254 255 254]

### median, average, std, mean, variance, histogram

numpy এ যে কোন array এর মধ্যমা, গড়, মধ্যক, আদর্শ বিচ্যুতি, বৈষম্য, বারলেখ বাহির করা যায়।

<font color="red"> Example : </font>

```python
import numpy as np

a = np.random.randint(low = 0, high = 10, size = 10)
print(a, "\n")

print("median : \n", np.median(a), "\n")

print("average : \n ", np.average(a), "\n")

print("mean : \n ",np.mean(a), "\n")

print("standard deviation : \n ", np.std(a), "\n")

print("variance : \n ", np.var(a), "\n")

print("histogram : \n ", np.histogram(a), "\n")

```

<font color="red"> Output : </font>

    [2 2 3 9 8 5 3 9 7 5]

    median :
     5.0

    average :
      5.3

    mean :
      5.3

    standard deviation :
      2.6476404589747453

    variance :
      7.010000000000001

    histogram :
      (array([2, 2, 0, 0, 2, 0, 0, 1, 1, 2]), array([2. , 2.7, 3.4, 4.1, 4.8, 5.5, 6.2, 6.9, 7.6, 8.3, 9. ]))

### Numpy writing , save and reading files

numpy ব্যবহার করে যে কোন data কে পরবর্তীতে ব্যবহার করার জন্য .npy file আকারে save করে রাখা যায়।

file save করার জন্য :
<font color="green"> numpy.save('fileName.npy', data) </font>

saved file open করার জন্য :
<font color="green"> numpy.load('fileName.npy') </font>

<font color="red"> Example : </font>

```python
import numpy as np
x = np.arange(100)
print(x)

np.save('test.npy', x)
```

<font color="red"> Output : </font>

    [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
     24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47
     48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71
     72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95
     96 97 98 99]

<mark> open save file </mark>

```python

data = np.load('test.npy')
print(data)
```

<font color="red"> Output : </font>

    [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23
     24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47
     48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71
     72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95
     96 97 98 99]

## Reading the data from a CSV file

.loadtxt() ব্যবহার করে numpy লাইব্রেরি text-file থেকে data pick করতে পারে।

<font color="green"> numpy.loadtxt(fname, dtype=<class 'float'>, comments='#', delimiter=None, converters=None, skiprows=0, usecols=None, unpack=False, ndmin=0, encoding='bytes', max_rows=None) </font>

-   fname = file name যে ফাইল এর data নাওয়া হবে।
-   delimiter = 'symble' যে symble অনুজায়ে data split করা হবে।
-   skiprows = number_of_row_to_skip যে সব রো বাদ দিব তার index number দিতে হবে।
-   usecols = number_of_column_to_use যে সব column ব্যবহার করতে চাই তা ।

besicaly এই সব parameter use হয়। তাই সব parameter নিয়ে আলোচনা করলাম না।

<font color="red"> example: </font>

```python
import numpy as np
data = np.loadtxt('data.csv', delimiter=',')
print(data)

print(type(data), "\n\n")

data = np.loadtxt('data.csv', delimiter=',',
                 skiprows=3, usecols=[1, 3])
print(data)
```

<font color="red"> Output : </font>

    [[  0.   1.  18.   2.]
     [  1.   6.   1.   3.]
     [  2.   3. 154.   0.]
     [  4. 978.   3.   6.]
     [  5.   2.  41.  45.]
     [  6.  67.   2.   3.]
     [  7.   5.  67.   2.]]
    <class 'numpy.ndarray'>


    [[978.   6.]
     [  2.  45.]
     [ 67.   3.]
     [  5.   2.]]

## Set Operations

### .unique()

যে কোন array এর সকল unique value গুলো পাওয়ার জন্য <font color="green"> numpy.unique(array) </font>
ব্যবহার করা হয়।

<font color="red"> example: </font>

```python
import numpy as np
data = np.array([1, 2, 3, 3, 2, 1, 4, 5])
print(np.unique(data),'\n\n' )

data = np.array([[1, 2, 3],
                [3, 2, 1],
                [4, 5, 3]])
print(np.unique(data))
```

<font color="red"> Output : </font>

    [1 2 3 4 5]


    [1 2 3 4 5]

### .in1d()

কোন array এর মধ্যে specific data বা array আছে কি না তা check করার জন্য <font color="green"> numpy.in1d(array,target) </font> ব্যবহার করা হয়।

<font color="red"> example </font>

```python
import numpy as np

data = np.array([0, 1, 2, 3, 4,1])
a = np.array([1, 2])
check = np.in1d(data, a)
print(check, "\n")
print(data[check])
```

<font color="red"> Output : </font>

    [False  True  True False False  True]

    [1 2 1]

### .intersect1d() , .setdiff1d() , .setxor1d() , .union1d()

-   ২টি array এর মধ্যে set intersection করতে <font color="green"> numpy.intersect1d(array1, array2) </font> ব্যবহৃত হয়।
-   ২টি array এর মধ্যে set difference বাহির করতে <font color="green"> numpy.setdiff1d(array1, array2) </font> ব্যবহৃত হয়।
-   ২টি array এর মধ্যে set exclusive-or বাহির করতে <font color="green"> numpy.setxor1d(array1, array2) </font> ব্যবহৃত হয়।
-   ২টি array এর মধ্যে set union বাহির করতে <font color="green"> numpy.union1d(array1, array2) </font> ব্যবহৃত হয়।

<font color="red"> example </font>

```python
import numpy as np

data1 = np.array([0, 1, 1, 3])
data2 = np.array([1, 2, 2, 3])
print(np.intersect1d(data1, data2))

print(np.setdiff1d(data2, data1))   # Minus operation/ Set difference

print(np.setxor1d(data1, data2))

print(np.setxor1d(data2, data1))

print(np.union1d(data1, data2))

```

<font color="red"> Output : </font>

    [1 3]
    [2]
    [0 2]
    [0 2]
    [0 1 2 3]

## Sorting with NumPy

numpy ব্যবহার করে multi-dimention array কে sort করা যায়। <font color="green"> numpy.sort(a, axis=-1, kind=None, order=None) </font>

<Mark> axis = 0 means columns </mark>

<Mark> axis = 1 means rows </mark>

axis = -1 defaultly sort করে last axis অনুযায়ী।

<font color="red"> example </font>

```python
import numpy as np
data = np.array([[2, 1, 3, 4],
                 [3, 1, 2, 0],
                 [5, 4, 0, 1]])
print("sort : \n", np.sort(data), "\n")   # sort along the last axis

print("sort by columns : \n", np.sort(data, axis = 0), "\n")

print("sort by rows : \n", np.sort(data, axis = 1), "\n")

# using order
dtype = [('name', 'S10'), ('height', float), ('age', int)]
values = [('Arthur', 1.8, 41), ('Lancelot', 1.9, 38),('Galahad', 1.7, 38)]
a = np.array(values, dtype=dtype)  # create a structured array
print("sort by height : \n", np.sort(a, order='height'))

```

<font color="red"> Output : </font>

    sort :
     [[1 2 3 4]
     [0 1 2 3]
     [0 1 4 5]]

    sort by columns :
     [[2 1 0 0]
     [3 1 2 1]
     [5 4 3 4]]

    sort by rows :
     [[1 2 3 4]
     [0 1 2 3]
     [0 1 4 5]]

    sort by height :
     [(b'Galahad', 1.7, 38) (b'Arthur', 1.8, 41) (b'Lancelot', 1.9, 38)]

## Count Non Zero Element

একটি array এর মধ্যে non-zero element গুলো count করার জন্য <font color="green"> numpy.count_nonzero(a, axis=None, \*, keepdims=False) </font> ব্যবহার করা হয়।

<font color="red"> example </font>

```python
import numpy as np
data = np.array([[1, 2, 6, 0, 0],
                [4, 0, 0, 1, 56]])
print(np.count_nonzero(data))

print(np.count_nonzero(data, axis = 0))

print(np.count_nonzero(data, axis = 1))
```

<font color="red"> Output : </font>

    6
    [2 1 1 1 1]
    [3 3]
