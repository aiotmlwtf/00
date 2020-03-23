---
title: jnotes
description: 
published: 1
date: 2020-03-23T07:49:09.085Z
tags: 
---


random forest

pca
svm

drive/collab

  <a href="https://colab.research.google.com/drive/1emF4dis543UHBkSpsUp5fiewk8BWVtDa" target="blank">collab file access</a>

<a href="" target="blank">ml4a</a>

<a href="https://colab.research.google.com/drive/1oHIf_gvp8o9YgaNfPGMVQM0uv7nE0Uwk" target="blank">public collab file</a> 
  
  <a href="  https://colab.research.google.com/drive/1oHIf_gvp8o9YgaNfPGMVQM0uv7nE0Uwk#scrollTo=TH36vrLqH5nl
" target="blank">indiv cell</a>  
</div>


<details>
  <summary>0001 python</summary>
  
python data types
containers, lists, dictionaries, sets, tuples, functions, classes

## numbers
Integers and floats work as you would expect from other languages:

```python
x = 3
print(x, type(x))

print(x + 1)   # Addition;
print(x - 1)   # Subtraction;
print(x * 2)   # Multiplication;
print(x ** 2)  # Exponentiation;

x += 1
print(x)
x *= 2
print(x)
y = 2.5
print(type(y))
print(y, y + 1, y * 2, y ** 2)
```

## booleans

Python implements Boolean logic using English words rather than symbols
(`&&`, `||`, etc.)

```python
t, f = True, False
print(type(t))

# the operations
print(t and f) # logical AND;
print(t or f)  # logical OR;
print(not t)   # logical NOT;
print(t != f)  # logical XOR;
```
## strings
```python
hello = 'hello'         # string literals can use single quotes
world = "anti-matter"   # or double quotes
print(hello, len(world))

hw = hello + ' ' + world  # string concatenation
print(hw)

hw12 = '%s %s %d' % (hello, world, 12)  # sprintf style string formatting
print(hw12)
```
## some string methods
```python
s = "hello"
print(s.capitalize())
print(s.upper())
print(s.rjust(7))      # right-justify, padding with spaces; prints "  hello"
print(s.center(7))     # center a string, padding with spaces; prints " hello "

# replace all instances of one substring with another;
print(s.replace('l', '(ell)'))

# strip leading and trailing whitespace; prints "world"
print('  world '.strip())

```
[more string methods](https://docs.python.org/3.8/library/stdtypes.html#string-methods)

## lists
A list is the Python equivalent of an array, but is resizeable and can contain elements of different types

```python
xs = [3, 1, 2]   # create a list
print(xs, xs[2])
print(xs[-1])     # negative indices count from the end of the list; prints "2"

xs[2] = 'foo'    # Lists can contain elements of different types
print(xs)

xs.append('bar') # Add a new element to the end of the list
print(xs)

x = xs.pop()     # Remove and return the last element of the list
print(x, xs)

```
[more on lists](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)


## slicing w

In addition to accessing list elements one at a time, Python provides concise syntax to access sublists; this is known as slicing:
```python
nums = range(5)    # range is a built-in function that creates a list of integers
print(nums)         # Prints "[0, 1, 2, 3, 4]"
print(nums[2:4])    # Get a slice from index 2 to 4 (exclusive); prints "[2, 3]"
print(nums[2:])     # Get a slice from index 2 to the end; prints "[2, 3, 4]"
print(nums[:2])     # Get a slice from the start to index 2 (exclusive); prints "[0, 1]"
print(nums[:])      # Get a slice of the whole list; prints ["0, 1, 2, 3, 4]"
print(nums[:-1])    # Slice indices can be negative; prints ["0, 1, 2, 3]"
nums[2:4] = [8, 9]  # Assign a new sublist to a slice
print(nums)         # Prints "[0, 1, 8, 9, 4]"
```

## loops

You can loop over the elements of a list like this:

```python
animals = ['cat', 'dog', 'monkey']
for animal in animals:
    print(animal)
```
## `enumerate`
access the index of each element within the body of a loop
```python
animals = ['cat', 'dog', 'monkey']
for idx, animal in enumerate(animals):
    print('#%d: %s' % (idx + 1, animal))
```
## list comprehensions w

transform one type of data into another. eg. computes square numbers
```python
nums = [0, 1, 2, 3, 4]
squares = []
for x in nums:
    squares.append(x ** 2)
print squares
```
```python
#  simpler using a list comprehension:"""
nums = [0, 1, 2, 3, 4]
squares = [x ** 2 for x in nums]
print squares

# List comprehensions can also contain conditions:
nums = [0, 1, 2, 3, 4]
even_squares = [x ** 2 for x in nums if x % 2 == 0]
print even_squares
```

## dictionaries w

A dictionary stores (key, value) pairs, similar to a `Map` in Java or an object in Javascript

```
d = {'cat': 'cute', 'dog': 'furry'}  # Create a new dictionary with some data
print d['cat']       # Get an entry from a dictionary; prints "cute"
print 'cat' in d     # Check if a dictionary has a given key; prints "True"

d['fish'] = 'wet'    # Set an entry in a dictionary
print d['fish']      # Prints "wet"

print d['monkey']  # KeyError: 'monkey' not a key of d

print d.get('monkey', 'N/A')  # Get an element with a default; prints "N/A"
print d.get('fish', 'N/A')    # Get an element with a default; prints "wet"

del d['fish']        # Remove an element from a dictionary
print d.get('fish', 'N/A') # "fish" is no longer a key; prints "N/A"

```
[documentation](https://docs.python.org/2/library/stdtypes.html#dict)

## iterate over the keys in a dictionary

```python
d = {'person': 2, 'cat': 4, 'spider': 8}
for animal in d:
    legs = d[animal]
    print 'A %s has %d legs' % (animal, legs)
```

## iteritems
access keys and their corresponding values
```python
d = {'person': 2, 'cat': 4, 'spider': 8}
for animal, legs in d.iteritems():
    print 'A %s has %d legs' % (animal, legs)

# Dictionary comprehensions: These are similar to list comprehensions, but allow you to easily construct dictionaries. For example:

nums = [0, 1, 2, 3, 4]
even_num_to_square = {x: x ** 2 for x in nums if x % 2 == 0}
print even_num_to_square

```

## sets w

A set is an unordered collection of distinct elements
```python
animals = {'cat', 'dog'}
print 'cat' in animals   # Check if an element is in a set; prints "True"
print 'fish' in animals  # prints "False"

animals.add('fish')      # Add an element to a set
print 'fish' in animals
print len(animals)       # Number of elements in a set;

animals.add('cat')       # Adding an element that is already in the set does nothing
print len(animals)       
animals.remove('cat')    # Remove an element from a set
print len(animals)

```
## loops
Iterating over a set has the same syntax as iterating over a list; however since sets are unordered, you cannot make assumptions about the order in which you visit the elements of the set
```python
animals = {'cat', 'dog', 'fish'}
for idx, animal in enumerate(animals):
    print '#%d: %s' % (idx + 1, animal)
# Prints "#1: fish", "#2: dog", "#3: cat"

```
## set comprehensions
Like lists and dictionaries, we can easily construct sets using set comprehensions
```python
from math import sqrt
print {int(sqrt(x)) for x in range(30)}
```


## tuples w
A tuple is an (immutable) ordered list of values. A tuple is similar to a list; one difference is that tuples can be used as keys in dictionaries and as elements of sets, while lists cannot.
```python
d = {(x, x + 1): x for x in range(10)}  # Create a dictionary with tuple keys
t = (5, 6)       # Create a tuple
print type(t)
print d[t]       
print d[(1, 2)]

t[0] = 1
```

## functions w
 functions are defined using the `def` keyword
```python
def sign(x):
    if x > 0:
        return 'positive'
    elif x < 0:
        return 'negative'
    else:
        return 'zero'

for x in [-1, 0, 1]:
    print(sign(x))
```

## ... with keyword arguments
```python
def hello(name, loud=False):
    if loud:
        print 'HELLO, %s' % name.upper()
    else:
        print 'Hello, %s!' % name

hello('Bob')
hello('Fred', loud=True)
```

## classes w
```python
class Greeter:

    # Constructor
    def __init__(self, name):
        self.name = name  # Create an instance variable

    # Instance method
    def greet(self, loud=False):
        if loud:
            print 'HELLO, %s!' % self.name.upper()
        else:
            print 'Hello, %s' % self.name

g = Greeter('Fred')  # Construct an instance of the Greeter class
g.greet()            # Call an instance method; prints "Hello, Fred"
g.greet(loud=True)   # Call an instance method; prints "HELLO, FRED!"

```



### huh


```python


"""# file access
handling files in collab (drive/github/local)

## Open files from your local file system

`files.upload` returns a dictionary of the files which were uploaded.
The dictionary is keyed by the file name, the value is the data which was uploaded.
"""

from google.colab import files

uploaded = files.upload()

for fn in uploaded.keys():
  print('User uploaded file "{name}" with length {length} bytes'.format(
      name=fn, length=len(uploaded[fn])))

"""## Inspect the file we downloaded to /tmp
!cat /tmp/downloaded_from_gcs.txt
"""

"""# Downloading files to your local file system
`files.download` will invoke a browser download of the file to your local computer.
"""

from google.colab import files

with open('example.txt', 'w') as f:
  f.write('some content')

files.download('example.txt')

"""## Open files from GitHub
to access files from a private repo, you must use a [GitHub access token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line).
"""

# Fetch a single <1MB file using the raw GitHub URL.
!curl --remote-name \
     -H 'Accept: application/vnd.github.v3.raw' \
     --location https://api.github.com/repos/jakevdp/PythonDataScienceHandbook/contents/notebooks/data/california_cities.csv

# Commented out IPython magic to ensure Python compatibility.
!git clone -l -s git://github.com/jakevdp/PythonDataScienceHandbook.git cloned-repo
# %cd cloned-repo
!ls

!git clone -l -s https://github.com/ml4a/ml4a-guides.git ml4a

# Commented out IPython magic to ensure Python compatibility.
# %cd ml4a
!ls





"""## google drive

## open files from Google Drive

The example below shows how to mount your Google Drive in your virtual machine using an authorization code.
"""

# Commented out IPython magic to ensure Python compatibility.
from google.colab import drive
drive.mount('/gdrive')
# %cd /gdrive

"""## Mounting Google Drive in your VM

The example below shows how to mount your Google Drive in your virtual machine using an authorization code, and shows a couple of ways to write & read files there. Once executed, observe the new file (`foo.txt`) is visible in https://drive.google.com/

Note this only supports reading and writing files.
"""

from google.colab import drive
drive.mount('/gdrive')

with open('/gdrive/My Drive/foo.txt', 'w') as f:
  f.write('Hello Google Drive!')
!cat '/gdrive/My Drive/foo.txt'

"""## Saving data to Google Drive

* [PyDrive reference](https://pythonhosted.org/PyDrive/)
* [Google Drive API reference](https://developers.google.com/drive/v3/reference/)
"""

# Import PyDrive and associated libraries.
# This only needs to be done once in a notebook.
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials

# Authenticate and create the PyDrive client.
# This only needs to be done once in a notebook.
auth.authenticate_user()
gauth = GoogleAuth()
gauth.credentials = GoogleCredentials.get_application_default()
drive = GoogleDrive(gauth)

# Create & upload a text file.
uploaded = drive.CreateFile({'title': 'Sample file.txt'})
uploaded.SetContentString('Sample upload file content')
uploaded.Upload()
print('Uploaded file with ID {}'.format(uploaded.get('id')))

"""After executing the cell above, a new file named 'Sample file.txt' will appear in your [drive.google.com](https://drive.google.com/) file list.

## Listing files in Google Drive
"""

# Import PyDrive and associated libraries.
# This only needs to be done once per notebook.
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials

# Authenticate and create the PyDrive client.
# This only needs to be done once per notebook.
auth.authenticate_user()
gauth = GoogleAuth()
gauth.credentials = GoogleCredentials.get_application_default()
drive = GoogleDrive(gauth)

# List .txt files in the root.
#
# Search query reference:
# https://developers.google.com/drive/v2/web/search-parameters
listed = drive.ListFile({'q': "title contains '.txt' and 'root' in parents"}).GetList()
for file in listed:
  print('title {}, id {}'.format(file['title'], file['id']))

"""## Downloading files or importing data from Google Drive

* [PyDrive reference](https://pythonhosted.org/PyDrive/)
* [Google Drive API reference](https://developers.google.com/drive/v3/reference/)
"""

# Import PyDrive and associated libraries.
# This only needs to be done once per notebook.
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive
from google.colab import auth
from oauth2client.client import GoogleCredentials

# Authenticate and create the PyDrive client.
# This only needs to be done once per notebook.
auth.authenticate_user()
gauth = GoogleAuth()
gauth.credentials = GoogleCredentials.get_application_default()
drive = GoogleDrive(gauth)

# Download a file based on its file ID.
#
# A file ID looks like: laggVyWshwcyP6kEI-y_W3P8D26sz
file_id = 'REPLACE_WITH_YOUR_FILE_ID'
downloaded = drive.CreateFile({'id': file_id})
print('Downloaded content "{}"'.format(downloaded.GetContentString()))







"""# random

## haiku
"""

from random import randint
wordList1 = ["Enchanting", "Amazing", "Colourful", "Delightful", "Delicate"]
wordList2 = ["visions", "distance", "conscience", "process", "chaos"]
wordList3 = ["superstitious", "contrasting", "graceful", "inviting", "contradicting", "overwhelming"]
wordList4 = ["true", "dark", "cold", "warm", "great"]
wordList5 = ["scenery","season", "colours","lights","Spring","Winter","Summer","Autumn"]
wordList6 = ["undeniable", "beautiful", "irreplaceable", "unbelievable", "irrevocable"]
wordList7 = ["inspiration", "imagination", "wisdom", "thoughts"]
wordIndex1=randint(0, len(wordList1)-1)
wordIndex2=randint(0, len(wordList2)-1)
wordIndex3=randint(0, len(wordList3)-1)
wordIndex4=randint(0, len(wordList4)-1)
wordIndex5=randint(0, len(wordList5)-1)
wordIndex6=randint(0, len(wordList6)-1)
wordIndex7=randint(0, len(wordList7)-1)
haiku = wordList1[wordIndex1] + " " + wordList2[wordIndex2] + ",\n" 
haiku = haiku + wordList3[wordIndex3] + " " + wordList4[wordIndex4] + " " + wordList5[wordIndex5]  + ",\n"
haiku = haiku + wordList6[wordIndex6] + " " + wordList7[wordIndex7] + "."
print(haiku)

"""# fractals

## mandelbrot computation using numpy
"""

from matplotlib.pyplot import imshow
from numpy import *
import time

def mandel(n, m, itermax, xmin, xmax, ymin, ymax):

    # The point of ix and iy is that they are 2D arrays
    # giving the x-coord and y-coord at each point in the array. 
    # The reason for doing this will become clear below...
    ix, iy = mgrid[0:n, 0:m]

    # Now x and y are the x-values and y-values at each
    # point in the array, linspace(start, end, n)
    # is an array of n linearly spaced points between
    # start and end, and we then index this array using
    # numpy fancy indexing. If A is an array and I is
    # an array of indices, then A[I] has the same shape
    # as I and at each place i in I has the value A[i].
    x = linspace(xmin, xmax, n)[ix]
    y = linspace(ymin, ymax, m)[iy]

    # c is the complex number with the given x, y coords
    c = x+complex(0,1)*y
    del x, y # save a bit of memory, we only need z

    # the output image coloured according to the number
    # of iterations it takes to get to the boundary
    # abs(z)>2
    img = zeros(c.shape, dtype=int)

    # Here is where the improvement over the standard
    # algorithm for drawing fractals in numpy comes in.
    # We flatten all the arrays ix, iy and c. This
    # flattening doesn't use any more memory because
    # we are just changing the shape of the array, the
    # data in memory stays the same. It also affects
    # each array in the same way, so that index i in
    # array c has x, y coords ix[i], iy[i]. The way the
    # algorithm works is that whenever abs(z)>2 we
    # remove the corresponding index from each of the
    # arrays ix, iy and c. Since we do the same thing
    # to each array, the correspondence between c and
    # the x, y coords stored in ix and iy is kept.
    ix.shape = n*m
    iy.shape = n*m
    c.shape = n*m

    # we iterate z->z^2+c with z starting at 0, but the
    # first iteration makes z=c so we just start there.
    # We need to copy c because otherwise the operation
    # z->z^2 will send c->c^2.
    z = copy(c)
    for i in range(itermax):
        if not len(z): break # all points have escaped

        # equivalent to z = z*z+c but quicker and uses
        # less memory
        multiply(z, z, z)
        add(z, c, z)

        # these are the points that have escaped
        rem = abs(z)>2.0

        # colour them with the iteration number, we
        # add one so that points which haven't
        # escaped have 0 as their iteration number,
        # this is why we keep the arrays ix and iy
        # because we need to know which point in img
        # to colour
        img[ix[rem], iy[rem]] = i+1

        # -rem is the array of points which haven't
        # escaped, in numpy -A for a boolean array A
        # is the NOT operation.
        # rem = -rem
        rem = logical_not(rem)
        # So we select out the points in
        # z, ix, iy and c which are still to be
        # iterated on in the next step
        z = z[rem]
        ix, iy = ix[rem], iy[rem]
        c = c[rem]
    return img

# (n, m): output image dimensions
# itermax: maximum number of iterations to do
# xmin, xmax, ymin, ymax: specify the region of the set to compute

I = mandel(400, 400, 59, -2, .5, -1.25, 1.25)
I[I==0] = 101
img = imshow(I.T, origin='lower left')# colormap
img.write_png('mandel.png')

"""## Julia fractals"""

from PIL import Image
from IPython.display import Image as Jimg, display

import random
# image size
imgx = 512
imgy = 512
image = Image.new("RGB", (imgx, imgy))

# drawing area
xa = -2.0
xb = 2.0
ya = -1.5
yb = 1.5
maxIt = 255 # max iterations allowed

# find a good Julia set point using the Mandelbrot set
while True:
    cx = random.random() * (xb - xa) + xa
    cy = random.random() * (yb - ya) + ya
    c = cx + cy * 1j
    z = c
    for i in range(maxIt):
        if abs(z) > 2.0:
            break 
        z = z * z + c
    if i > 10 and i < 100:
        break

# draw the Julia set
for y in range(imgy):
    zy = y * (yb - ya) / (imgy - 1)  + ya
    for x in range(imgx):
        zx = x * (xb - xa) / (imgx - 1)  + xa
        z = zx + zy * 1j
        for i in range(maxIt):
            if abs(z) > 2.0:
                break 
            z = z * z + c
        image.putpixel((x, y), (i % 8 * 32, i % 16 * 16, i % 32 * 8))

image.save("fractal.julia.png", "PNG")
display(Jimg('fractal.julia.png'))

"""life

## IFS fractals w/ automatic probability distribution

http://en.wikipedia.org/wiki/Iterated_function_system

http://en.wikipedia.org/wiki/Chaos_game
"""

import random
from PIL import Image

# calcultae area of polygon ( http://en.wikipedia.org/wiki/Shoelace_formula )
# corners must be ordered in clockwise or counter-clockwise direction
def PolygonArea(corners):
    n = len(corners) # of corners
    area = 0.0
    for i in range(n):
        j = (i + 1) % n
        area += corners[i][0] * corners[j][1]
        area -= corners[j][0] * corners[i][1]
    area = abs(area) / 2.0
    return area

def IFS(x, y, i): # apply ith transformation to given point
    x0 = x * mat[i][0] + y * mat[i][1] + mat[i][4] 
    y  = x * mat[i][2] + y * mat[i][3] + mat[i][5] 
    x = x0
    return (x, y)

# use dictionary
fractalName = "barnsleyfern"
mat=[[0.0, 0.0, 0.0, 0.16, 0.0, 0.0],
    [0.85, 0.04, -0.04, 0.85, 0.0, 1.6],
    [0.2, -0.26, 0.23, 0.22, 0.0, 1.6],
    [-0.15, 0.28, 0.26, 0.24, 0.0, 0.44]]
    
fractalName = "dragoncurve"
mat = [[0.5, -0.5, 0.5, 0.5, 0.0, 0.0],
      [-0.5, -0.5, 0.5, -0.5, 1.0, 0.0]]
      
fractalName = "centipede"
mat = [[0.824074, 0.281482, -0.212346,  0.864198, -1.882290, -0.110607],
       [0.088272, 0.520988, -0.463889, -0.377778,  0.785360,  8.095795]]

fractalName = "sierpinskitriangle"

mat = [[0.5, 0.0, 0.0, 0.5, 0.0, 0.0],
       [0.5, 0.0, 0.0, 0.5, 0.5, 0.0],
       [0.5, 0.0, 0.0, 0.5, 0.0, 0.5]]
       
fractalName = "levyccurve"
mat = [[0.5, -0.5, 0.5, 0.5, 0.0, 0.0],
      [0.5, 0.5, -0.5, 0.5, 0.5, 0.5]]

imgx = 512
imgy = 512 # will be auto-re-adjusted according to aspect ratio of the fractal
maxIt = imgx * imgy * 2

m = len(mat) # number of IFS transformations

# calculate probabilities of the transformations
areas = [] # areas of transformed rectangles
for j in range(m):
    area = PolygonArea([IFS(1, 1, j), IFS(-1, 1, j), IFS(-1, -1, j), IFS(1, -1, j)])
    areas.append(area)

totalArea = sum(areas)

pArr = []

for j in range(m):
    pArr.append(areas[j] / totalArea)
     
# find bounding rectangle of the fractal using Chaos Game algorithm
x = mat[0][4]
y = mat[0][5] 
xa = x
xb = x
ya = y
yb = y

for k in range(maxIt):
    i = random.randint(0, m - 1)
    if random.random() <= pArr[i]:
        (x, y) = IFS(x, y, i)
        if x < xa:
            xa = x
        if x > xb:
            xb = x
        if y < ya:
            ya = y
        if y > yb:
            yb = y

imgy = int(imgy * (yb - ya) / (xb - xa)) # re-adjust the aspect ratio 
image = Image.new("RGB", (imgx, imgy))
pixels = image.load()

# drawing using Chaos Game algorithm
theColor = (255, 255, 255)
x=0.0
y=0.0 
for k in range(maxIt):
    i = random.randint(0, m - 1)
    if random.random() <= pArr[i]:
        (x, y) = IFS(x, y, i)
        jx = int((x - xa) / (xb - xa) * (imgx - 1)) 
        jy = (imgy - 1) - int((y - ya) / (yb - ya) * (imgy - 1))
        if jx >= 0 and jx < imgx and jy >= 0 and jy < imgy:
            pixels[jx, jy] = theColor

from IPython.display import Image as Jimg, display

filename = fractalName + ".fractal.png"
image.save(filename, "PNG")
print(filename)
print("Probabilities: " + str(pArr))

display(Jimg('/content/' + filename))



"""# datascience 010001

## numpy matplotlib pandas

**Scipy** and **numpy** are libraries for efficient and fast numeric computing. **Matplotlib** is a plotting library, inspired by MATLAB.

___
**Pyplot** is an interactive api for matplotlib, for use in notebooks like jupyter. 
use it like this: 
import matplotlib.pyplot as plt.

pylab is part of matplotlib (in matplotlib.pylab) and tries to give you a MatLab like environment)
- an automatic import will put all symbols from matplotlib.pylab into global scope
- numpy gets imported under the np alias
- Symbols from matplotlib are available under the mpl alias

___
**ipython --pylab**

## 0010 numpy w
`numpy arrays, array indexing, datatypes, array math, broadcasting`

Numpy is the core library for scientific computing in Python. It provides a high-performance multidimensional array object, and tools for working with these arrays. If you are already familiar with MATLAB, you might find this [tutorial](http://wiki.scipy.org/NumPy_for_Matlab_Users) useful to get started with Numpy.

To use Numpy, we first need to import the `numpy` package:
"""

import numpy as np

"""###Arrays

A numpy array is a grid of values, all of the same type, and is indexed by a tuple of nonnegative integers. The number of dimensions is the rank of the array; the shape of an array is a tuple of integers giving the size of the array along each dimension.

We can initialize numpy arrays from nested Python lists, and access elements using square brackets:
"""

a = np.array([1, 2, 3])  # Create a rank 1 array
print type(a), a.shape, a[0], a[1], a[2]
a[0] = 5                 # Change an element of the array
print a

b = np.array([[1,2,3],[4,5,6]])   # Create a rank 2 array
print b

print b.shape                   
print b[0, 0], b[0, 1], b[1, 0]

"""Numpy also provides many functions to create arrays:"""

a = np.zeros((2,2))  # Create an array of all zeros
print a

b = np.ones((1,2))   # Create an array of all ones
print b

c = np.full((2,2), 7) # Create a constant array
print c

d = np.eye(2)        # Create a 2x2 identity matrix
print d

e = np.random.random((2,2)) # Create an array filled with random values
print e

"""###Array indexing

Numpy offers several ways to index into arrays.

Slicing: Similar to Python lists, numpy arrays can be sliced. Since arrays may be multidimensional, you must specify a slice for each dimension of the array:
"""

import numpy as np

# Create the following rank 2 array with shape (3, 4)
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]
a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])

# Use slicing to pull out the subarray consisting of the first 2 rows
# and columns 1 and 2; b is the following array of shape (2, 2):
# [[2 3]
#  [6 7]]
b = a[:2, 1:3]
print b

"""A slice of an array is a view into the same data, so modifying it will modify the original array."""

print a[0, 1]  
b[0, 0] = 77    # b[0, 0] is the same piece of data as a[0, 1]
print a[0, 1]

"""You can also mix integer indexing with slice indexing. However, doing so will yield an array of lower rank than the original array. Note that this is quite different from the way that MATLAB handles array slicing:"""

# Create the following rank 2 array with shape (3, 4)
a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])
print a

"""Two ways of accessing the data in the middle row of the array.
Mixing integer indexing with slices yields an array of lower rank,
while using only slices yields an array of the same rank as the
original array:
"""

row_r1 = a[1, :]    # Rank 1 view of the second row of a  
row_r2 = a[1:2, :]  # Rank 2 view of the second row of a
row_r3 = a[[1], :]  # Rank 2 view of the second row of a
print row_r1, row_r1.shape 
print row_r2, row_r2.shape
print row_r3, row_r3.shape

# We can make the same distinction when accessing columns of an array:
col_r1 = a[:, 1]
col_r2 = a[:, 1:2]
print col_r1, col_r1.shape
print
print col_r2, col_r2.shape

"""Integer array indexing: When you index into numpy arrays using slicing, the resulting array view will always be a subarray of the original array. In contrast, integer array indexing allows you to construct arbitrary arrays using the data from another array. Here is an example:"""

a = np.array([[1,2], [3, 4], [5, 6]])

# An example of integer array indexing.
# The returned array will have shape (3,) and 
print a[[0, 1, 2], [0, 1, 0]]

# The above example of integer array indexing is equivalent to this:
print np.array([a[0, 0], a[1, 1], a[2, 0]])

# When using integer array indexing, you can reuse the same
# element from the source array:
print a[[0, 0], [1, 1]]

# Equivalent to the previous integer array indexing example
print np.array([a[0, 1], a[0, 1]])

"""One useful trick with integer array indexing is selecting or mutating one element from each row of a matrix:"""

# Create a new array from which we will select elements
a = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
print a

# Create an array of indices
b = np.array([0, 2, 0, 1])

# Select one element from each row of a using the indices in b
print a[np.arange(4), b]  # Prints "[ 1  6  7 11]"

# Mutate one element from each row of a using the indices in b
a[np.arange(4), b] += 10
print a

"""Boolean array indexing: Boolean array indexing lets you pick out arbitrary elements of an array. Frequently this type of indexing is used to select the elements of an array that satisfy some condition. Here is an example:"""

import numpy as np

a = np.array([[1,2], [3, 4], [5, 6]])

bool_idx = (a > 2)  # Find the elements of a that are bigger than 2;
                    # this returns a numpy array of Booleans of the same
                    # shape as a, where each slot of bool_idx tells
                    # whether that element of a is > 2.

print bool_idx

# We use boolean array indexing to construct a rank 1 array
# consisting of the elements of a corresponding to the True values
# of bool_idx
print a[bool_idx]

# We can do all of the above in a single concise statement:
print a[a > 2]

"""For brevity we have left out a lot of details about numpy array indexing; if you want to know more you should read the documentation.

###Datatypes

Every numpy array is a grid of elements of the same type. Numpy provides a large set of numeric datatypes that you can use to construct arrays. Numpy tries to guess a datatype when you create an array, but functions that construct arrays usually also include an optional argument to explicitly specify the datatype. Here is an example:
"""

x = np.array([1, 2])  # Let numpy choose the datatype
y = np.array([1.0, 2.0])  # Let numpy choose the datatype
z = np.array([1, 2], dtype=np.int64)  # Force a particular datatype

print x.dtype, y.dtype, z.dtype

"""You can read all about numpy datatypes in the [documentation](http://docs.scipy.org/doc/numpy/reference/arrays.dtypes.html).

###Array math

Basic mathematical functions operate elementwise on arrays, and are available both as operator overloads and as functions in the numpy module:
"""

x = np.array([[1,2],[3,4]], dtype=np.float64)
y = np.array([[5,6],[7,8]], dtype=np.float64)

# Elementwise sum; both produce the array
print x + y
print np.add(x, y)

# Elementwise difference; both produce the array
print x - y
print np.subtract(x, y)

# Elementwise product; both produce the array
print x * y
print np.multiply(x, y)

# Elementwise division; both produce the array
# [[ 0.2         0.33333333]
#  [ 0.42857143  0.5       ]]
print x / y
print np.divide(x, y)

# Elementwise square root; produces the array
# [[ 1.          1.41421356]
#  [ 1.73205081  2.        ]]
print np.sqrt(x)

"""Note that unlike MATLAB, `*` is elementwise multiplication, not matrix multiplication. We instead use the dot function to compute inner products of vectors, to multiply a vector by a matrix, and to multiply matrices. dot is available both as a function in the numpy module and as an instance method of array objects:"""

x = np.array([[1,2],[3,4]])
y = np.array([[5,6],[7,8]])

v = np.array([9,10])
w = np.array([11, 12])

# Inner product of vectors; both produce 219
print v.dot(w)
print np.dot(v, w)

# Matrix / vector product; both produce the rank 1 array [29 67]
print x.dot(v)
print np.dot(x, v)

# Matrix / matrix product; both produce the rank 2 array
# [[19 22]
#  [43 50]]
print x.dot(y)
print np.dot(x, y)

"""Numpy provides many useful functions for performing computations on arrays; one of the most useful is `sum`:"""

x = np.array([[1,2],[3,4]])

print np.sum(x)  # Compute sum of all elements; prints "10"
print np.sum(x, axis=0)  # Compute sum of each column; prints "[4 6]"
print np.sum(x, axis=1)  # Compute sum of each row; prints "[3 7]"

"""You can find the full list of mathematical functions provided by numpy in the [documentation](http://docs.scipy.org/doc/numpy/reference/routines.math.html).

Apart from computing mathematical functions using arrays, we frequently need to reshape or otherwise manipulate data in arrays. The simplest example of this type of operation is transposing a matrix; to transpose a matrix, simply use the T attribute of an array object:
"""

print x
print x.T

v = np.array([[1,2,3]])
print v 
print v.T

"""###Broadcasting

Broadcasting is a powerful mechanism that allows numpy to work with arrays of different shapes when performing arithmetic operations. Frequently we have a smaller array and a larger array, and we want to use the smaller array multiple times to perform some operation on the larger array.

For example, suppose that we want to add a constant vector to each row of a matrix. We could do it like this:
"""

# We will add the vector v to each row of the matrix x,
# storing the result in the matrix y
x = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
v = np.array([1, 0, 1])
y = np.empty_like(x)   # Create an empty matrix with the same shape as x

# Add the vector v to each row of the matrix x with an explicit loop
for i in range(4):
    y[i, :] = x[i, :] + v

print y

"""This works; however when the matrix `x` is very large, computing an explicit loop in Python could be slow. Note that adding the vector v to each row of the matrix `x` is equivalent to forming a matrix `vv` by stacking multiple copies of `v` vertically, then performing elementwise summation of `x` and `vv`. We could implement this approach like this:"""

vv = np.tile(v, (4, 1))  # Stack 4 copies of v on top of each other
print vv                 # Prints "[[1 0 1]
                         #          [1 0 1]
                         #          [1 0 1]
                         #          [1 0 1]]"

y = x + vv  # Add x and vv elementwise
print y

"""Numpy broadcasting allows us to perform this computation without actually creating multiple copies of v. Consider this version, using broadcasting:"""

import numpy as np

# We will add the vector v to each row of the matrix x,
# storing the result in the matrix y
x = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
v = np.array([1, 0, 1])
y = x + v  # Add v to each row of x using broadcasting
print y

"""The line `y = x + v` works even though `x` has shape `(4, 3)` and `v` has shape `(3,)` due to broadcasting; this line works as if v actually had shape `(4, 3)`, where each row was a copy of `v`, and the sum was performed elementwise.

Broadcasting two arrays together follows these rules:

1. If the arrays do not have the same rank, prepend the shape of the lower rank array with 1s until both shapes have the same length.
2. The two arrays are said to be compatible in a dimension if they have the same size in the dimension, or if one of the arrays has size 1 in that dimension.
3. The arrays can be broadcast together if they are compatible in all dimensions.
4. After broadcasting, each array behaves as if it had shape equal to the elementwise maximum of shapes of the two input arrays.
5. In any dimension where one array had size 1 and the other array had size greater than 1, the first array behaves as if it were copied along that dimension

If this explanation does not make sense, try reading the explanation from the [documentation](http://docs.scipy.org/doc/numpy/user/basics.broadcasting.html) or this [explanation](http://wiki.scipy.org/EricsBroadcastingDoc).

Functions that support broadcasting are known as universal functions. You can find the list of all universal functions in the [documentation](http://docs.scipy.org/doc/numpy/reference/ufuncs.html#available-ufuncs).

Here are some applications of broadcasting:
"""

# Compute outer product of vectors
v = np.array([1,2,3])  # v has shape (3,)
w = np.array([4,5])    # w has shape (2,)
# To compute an outer product, we first reshape v to be a column
# vector of shape (3, 1); we can then broadcast it against w to yield
# an output of shape (3, 2), which is the outer product of v and w:

print np.reshape(v, (3, 1)) * w

# Add a vector to each row of a matrix
x = np.array([[1,2,3], [4,5,6]])
# x has shape (2, 3) and v has shape (3,) so they broadcast to (2, 3),
# giving the following matrix:

print x + v

# Add a vector to each column of a matrix
# x has shape (2, 3) and w has shape (2,).
# If we transpose x then it has shape (3, 2) and can be broadcast
# against w to yield a result of shape (3, 2); transposing this result
# yields the final result of shape (2, 3) which is the matrix x with
# the vector w added to each column. Gives the following matrix:

print (x.T + w).T

# Another solution is to reshape w to be a row vector of shape (2, 1);
# we can then broadcast it directly against x to produce the same
# output.
print x + np.reshape(w, (2, 1))

# Multiply a matrix by a constant:
# x has shape (2, 3). Numpy treats scalars as arrays of shape ();
# these can be broadcast together to shape (2, 3), producing the
# following array:
print x * 2

"""Broadcasting typically makes your code more concise and faster, so you should strive to use it where possible.

This brief overview has touched on many of the important things that you need to know about numpy, but is far from complete. Check out the [numpy reference](http://docs.scipy.org/doc/numpy/reference/) to find out much more about numpy.

## 0011 matplotlib w

`plotting, subplots, images`

Matplotlib is a plotting library. In this section give a brief introduction to the `matplotlib.pyplot` module, which provides a plotting system similar to that of MATLAB.
"""

import matplotlib.pyplot as plt

"""By running this special iPython command, we will be displaying plots inline:"""

# Commented out IPython magic to ensure Python compatibility.
# %matplotlib inline

"""###Plotting

The most important function in `matplotlib` is plot, which allows you to plot 2D data. Here is a simple example:
"""

# Compute the x and y coordinates for points on a sine curve
x = np.arange(0, 3 * np.pi, 0.1)
y = np.sin(x)

# Plot the points using matplotlib
plt.plot(x, y)

"""With just a little bit of extra work we can easily plot multiple lines at once, and add a title, legend, and axis labels:"""

y_sin = np.sin(x)
y_cos = np.cos(x)

# Plot the points using matplotlib
plt.plot(x, y_sin)
plt.plot(x, y_cos)
plt.xlabel('x axis label')
plt.ylabel('y axis label')
plt.title('Sine and Cosine')
plt.legend(['Sine', 'Cosine'])

"""###Subplots

You can plot different things in the same figure using the subplot function. Here is an example:
"""

# Compute the x and y coordinates for points on sine and cosine curves
x = np.arange(0, 3 * np.pi, 0.1)
y_sin = np.sin(x)
y_cos = np.cos(x)

# Set up a subplot grid that has height 2 and width 1,
# and set the first such subplot as active.
plt.subplot(2, 1, 1)

# Make the first plot
plt.plot(x, y_sin)
plt.title('Sine')

# Set the second subplot as active, and make the second plot.
plt.subplot(2, 1, 2)
plt.plot(x, y_cos)
plt.title('Cosine')

# Show the figure.
plt.show()

"""You can read much more about the `subplot` function in the [documentation](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.subplot)."""





"""## 0100 pandas"""

!wget https://pynative.com/wp-content/uploads/2019/01/Automobile_data.csv

# print first five rows from given data set
import pandas as pd
df = pd.read_csv("Automobile_data.csv")
df.head(5)

# last five rows
import pandas as pd
df = pd.read_csv("Automobile_data.csv")
df.tail(5)

# update CSV file, clean data; replace all column values which contain ‘?’ and n.a with NaN
df = pd.read_csv("Automobile_data.csv", na_values={
'price':["?","n.a"],
'stroke':["?","n.a"],
'horsepower':["?","n.a"],
'peak-rpm':["?","n.a"],
'average-mileage':["?","n.a"]})
print (df)

df.to_csv("Automobile_data2.csv")

# find the most expensive car company name
import pandas as pd
df = pd.read_csv("Automobile_data2.csv")
df = df [['company','price']][df.price==df['price'].max()]
df

#print All Toyota Cars details
import pandas as pd
df = pd.read_csv("Automobile_data.csv")
car_Manufacturers = df.groupby('company')
toyotaDf = car_Manufacturers.get_group('toyota')
toyotaDf

# count total cars per company
import pandas as pd
df = pd.read_csv("Automobile_data2.csv")
df['company'].value_counts()

# find each company’s most expensive car
import pandas as pd
df = pd.read_csv("Automobile_data2.csv")
car_Manufacturers = df.groupby('company')
priceDf = car_Manufacturers['company','price'].max()
priceDf

# find the average mileage of each car making company
import pandas as pd
df = pd.read_csv("Automobile_data2.csv")
car_Manufacturers = df.groupby('company')
mileageDf = car_Manufacturers['company','average-mileage'].mean()
mileageDf

# sort all cars by Price column
import pandas as pd
carsDf = pd.read_csv("Automobile_data2.csv")
carsDf = carsDf.sort_values(by=['price', 'horsepower'], ascending=False)
carsDf.head(5)

# create two data frames using two Dicts, concatenate those two data frames and create a key for each data frame
import pandas as pd
GermanCars = {'Company': ['Ford', 'Mercedes', 'BMV', 'Audi'], 'Price': [23845, 171995, 135925 , 71400]}
carsDf1 = pd.DataFrame.from_dict(GermanCars)

japaneseCars = {'Company': ['Toyota', 'Honda', 'Nissan', 'Mitsubishi '], 'Price': [29995, 23600, 61500 , 58900]}
carsDf2 = pd.DataFrame.from_dict(japaneseCars)

carsDf = pd.concat([carsDf1, carsDf2], keys=["Germany", "Japan"])
carsDf

# create two data frames using the following two dicts
# merge two data frames
# append second data frame as a new column to the first data frame
import pandas as pd

Car_Price = {'Company': ['Toyota', 'Honda', 'BMV', 'Audi'], 'Price': [23845, 17995, 135925 , 71400]}
carPriceDf = pd.DataFrame.from_dict(Car_Price)

car_Horsepower = {'Company': ['Toyota', 'Honda', 'BMV', 'Audi'], 'horsepower': [141, 80, 182 , 160]}
carsHorsepowerDf = pd.DataFrame.from_dict(car_Horsepower)

carsDf = pd.merge(carPriceDf, carsHorsepowerDf, on="Company")
carsDf
```
  
  </details>