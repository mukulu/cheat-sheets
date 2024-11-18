## Installation of numpy python
`pip install numpy`
## Initilizing dependecies
`import numpy as np`

## Slicing in python
```python
# sequence[start:stop:step] where start is 0 stop is exclusive i.e. mathematically [start:stop)
my_list =np.linspace(1,20,20).astype('int')
"""
array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16, 17,
       18, 19, 20])
"""
#note: start is from 0, so 2 is 3rd item
my_list[2:5] #lists 3rd item for 2 to 5th excludes 6th for 5
#i.e. array([3, 4, 5])
my_list[0:10:2] #lists 1st,3rd,5th,7th,9th,excludes 11th
array([1, 3, 5, 7, 9])
my_list[5:] #5: is from 6th item forward
"""
array([ 6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20])
"""
#Note: [:n] = [0:n] = [0:n,] and [n:] = [n:,]
#Note: [::2,], [:n:2,] or [n::2, ] is possible 2 is increment.

#Negative increment goes backward from starting point
my_list[::-1] #starts at the end backward by incr -1
"""
array([20, 19, 18, 17, 16, 15, 14, 13, 12, 11, 10,  9,  8,  7,  6,  5,  4,
        3,  2,  1])
"""
my_list[5::-2] #starts at 5 backward by increment -2
"""
array([6, 5, 4, 3, 2, 1])
"""
#in start:end:increment, start remains inclusive and end exclusive

"""Note:
size of my_list is 20, i.e last incr is 19th
when last incr is greater than size, incr stop at size
if incr is -1, and start is greater than size, starts at size.
Therefore:
my_list[0:20,] stops at my_list[0:19]
my_list[20::-1] starts at my_list[19::-1]
my_list[20:19:-1] would be my_list[19:19:-1] and 19 in limit becomes exclusive, thus empty []
my_list[20:18:-1] would be my_list[19:18:-1] and 18 in limit is exclusive, thus only 19th is displayed [20]

```

## Power of slicing in multidimension arrays
```python
my_list.reshape(5,4)
"""
array([[ 1,  2,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12],
       [13, 14, 15, 16],
       [17, 18, 19, 20]])
"""
my_list.reshape(5,4)[::-1,] #reverse outer-dim, ie. rows
"""
array([[17, 18, 19, 20],
       [13, 14, 15, 16],
       [ 9, 10, 11, 12],
       [ 5,  6,  7,  8],
       [ 1,  2,  3,  4]])
"""
my_list.reshape(5,4)[:,::-1] #reverse inner-dim, ie. columns
"""
array([[ 4,  3,  2,  1],
       [ 8,  7,  6,  5],
       [12, 11, 10,  9],
       [16, 15, 14, 13],
       [20, 19, 18, 17]])
"""
my_list.reshape(5,4)[::-1,::-1] #reverse of both
"""
array([[20, 19, 18, 17],
       [16, 15, 14, 13],
       [12, 11, 10,  9],
       [ 8,  7,  6,  5],
       [ 4,  3,  2,  1]])
"""
my_list.reshape(5,4)[::-2,::-2]
"""
array([[20, 18],
       [12, 10],
       [ 4,  2]])
"""
my_list.reshape(5,4)
"""
array([[ 1,  2,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12],
       [13, 14, 15, 16],
       [17, 18, 19, 20]])
"""
my_list.reshape(5,4)[:,0] #all rows/cells of 1st column
# array([ 1,  5,  9, 13, 17])
my_list.reshape(5,4)[0,:] #first row, all cells/column
# array([1, 2, 3, 4])
my_list.reshape(5,4)[0::-1,:]#if start is 0 & incr is -1, it does positive increment
# array([1, 2, 3, 4])
my_list.reshape(5,4)[:,0:-1] #from 0 row to last-but-1
"""
array([[ 1,  2,  3],
       [ 5,  6,  7],
       [ 9, 10, 11],
       [13, 14, 15],
       [17, 18, 19]])
"""
my_list.reshape(5,4)[0:-1,:] #from 0 row to last-but-1
"""
array([[ 1,  2,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12],
       [13, 14, 15, 16]])
"""
```


## Working with data types

```python
data_list = list(range(10)) #produce list
type(l) #displays <class 'list'>
int_val = 32 # <class 'int'>
string_list = [ str(item) for item in data_list]
type(string_list[0]) # <class 'str'>
bool_val = True #<class 'bool'>
float_val = 3.14 #<class 'float'>

#Enforcing types in numpy
np.array([1,2,3], dtype='float') #gives float64

#Working with range
range_vals = range(1,10,2) #prints range(1,10,2)
#range can be evaluated
3 in range_vals #evaluates True
4 in range_vals #evaluate False
list(range_vals) # returns [1, 3, 5, 7, 9]
[i for i in range(1,10,2)] # [1, 3, 5, 9]

[range(i,i+5) for i in range(6,24,3)]
"""
[range(6, 11), range(9, 14), range(12, 17), range(15, 20), range(18, 23), range(21, 26)]
"""
np.array([range(i,i+5) for i in range(6,24,3)])
"""
array([[ 6,  7,  8,  9, 10],
       [ 9, 10, 11, 12, 13],
       [12, 13, 14, 15, 16],
       [15, 16, 17, 18, 19],
       [18, 19, 20, 21, 22],
       [21, 22, 23, 24, 25]])
"""
[list(range(i,i+5)) for i in range(6,24,3)]
#coverts list object to lists
"""
[[6, 7, 8, 9, 10], [9, 10, 11, 12, 13], [12, 13, 14, 15, 16], [15, 16, 17, 18, 19], [18, 19, 20, 21, 22], [21, 22, 23, 24, 25]]
"""
#This converts range objects to np.array
np.array([range(i,i+5) for i in range(6,24,3)])
#This convert lists to the same np.array
np.array([list(range(i,i+5)) for i in range(6,24,3)])
```

## Creating arrays
Note: in array generation, in most cases the lower limit is always inclusive while upper is exclusive, except function that explicitly hint inclusivity of upper limit like np.linspace which generate evenly spaced values from low to high.

#### Creating using EMPTY method
*Not the best way to start arrays*
```python
array_1d_2 = np.empty(10)
#Results array(10,) of random floats
"""e.g.
array([4.90259864e-310, 0.00000000e+000, 6.22194860e-310, 6.22194860e-310,
       6.22194860e-310, 6.22194860e-310, 6.22194860e-310, 6.22194860e-310,
       6.22194860e-310, 6.22194860e-310])
"""
```

```python
array_1d_2 = np.empty((5,2)) 
#Results array(5,2) of random floats
"""e.g.
array([[4.90259864e-310, 0.00000000e+000],
       [6.22194860e-310, 6.22194860e-310],
       [6.22194860e-310, 6.22194860e-310],
       [6.22194860e-310, 6.22194860e-310],
       [6.22194860e-310, 6.22194860e-310]])
"""
```

```python
array_1d_3 = np.empty((5,2),dtype=int) 
#Results array(5,2) of integers
"""e.g.
array([[ 99229701223595,               0],
       [125933641650624, 125933641650688],
       [125933641650752, 125933641650816],
       [125933641650880, 125933641586864],
       [125933641586928, 125933641586992]])
"""
```

#### Creating an array with RANDOM method
**Using random.choice to pick from a pool of numbers**
```python
choice_pool=np.array([10,20,30])
random_array = np.random.choice(choice_pool,(4,3))
"""i.e. values 10,20 or 30 randomly filled
array([[20, 20, 20],
       [20, 10, 30],
       [10, 10, 20],
       [30, 20, 30]])
```

**Using random.randint() for randoms in range**
```python
array1 = np.random.randint(low=10,high=25, size=(5,3))
#same as np.random.randint(10,25,(5,3))
#Results array(5,3) of integers between 10 and 25
"""e.g.
array([[11, 21, 17],
       [17, 24, 12],
       [22, 12, 13],
       [16, 16, 21],
       [15, 19, 13]])
"""  
#for dim array(15,) this is also okay
# np.random.randint(10,25,15) or
# np.random.randint(10,25,size=15)
```

**Using random.uniform() for randoms in range**
```python
array2 = np.random.uniform(low=5.0,high=35.5, size=(5,4))
#Results array(5,4) of floats between 5.0 and 35.5
"""e.g. 
array([[ 5.09495838, 22.56258526, 20.3735947 ,  6.00518271],
       [17.40362912, 25.77751863,  5.10011415, 14.96059586],
       [27.3301079 , 29.53561485, 30.45748392, 18.80975869],
       [16.14600552, 12.79878534, 18.46192491,  6.35517947],
       [27.3189985 , 24.9977    , 15.45182483, 15.41747396]])
"""
```

**Floats from random.uniform() can be rounded to fixed decimals**
```python
array2 = np.random.uniform(low=0.1,high=0.9, size=(4,3)).round(2)
#same as np.random.uniform(0.1,0.9,(4,3)).round(2)
#Results array(4,3) of floats between 0.1 and 0.9 with two decimals
"""e.g.
array([[0.63, 0.21, 0.6 ],
       [0.11, 0.78, 0.35],
       [0.34, 0.83, 0.14],
       [0.73, 0.79, 0.4 ]])
"""
```
**Array of floats can be rounded in two ways**
```python
array2 = np.random.uniform(low=0.001, high=99.999, size=(6,3))
np.round(array2,3) #produce 3 decimals array without altering array2
array2.round(3) #alters permanetly array2 to have only 3 decimals
#i.e. array2 will no longer have many decimals after array2.round(3)
#     but will still have many decimals if only passed np.round(array2,3)
"""e.g.
array([[11.79956327, 71.61252304, 96.094405  ],
       [54.15313696, 56.23371537, 40.44040395],
       [72.40971487, 95.1500104 , 37.03052551],
       [89.58433318, 94.59624901, 89.14742412],
       [84.90547667, 95.68895713, 31.29925878],
       [92.20947871, 11.81958509, 65.08119331]])
	   
array([[11.8  , 71.613, 96.094],
       [54.153, 56.234, 40.44 ],
       [72.41 , 95.15 , 37.031],
       [89.584, 94.596, 89.147],
       [84.905, 95.689, 31.299],
       [92.209, 11.82 , 65.081]])
"""
```
**Using random.normal for normal (gausian) distribution**
```python
#loc is the center(mean of the distribution)
#scale is the standard deviation (spread/width)
#size is the output shape of the array
distrib_a = np.random.normal(loc=0.0,scale=1.0,size=(5,4))
"""
array([[ 0.1238856 ,  0.45042249,  0.53363055,  0.3238294 ],
       [-0.8636228 , -0.16273923,  0.44301145, -0.60470517],
       [-0.3003054 ,  0.14679978, -1.40713515, -0.30070459],
       [ 0.62356528, -1.14129804,  1.87775547, -1.39716645],
       [-0.8718562 , -1.01970921,  0.32497037, -0.99441224]])
"""


```

## Making array copies
```python
sample_array = np.arange(5) #array([0, 1, 2, 3, 4])
a_copy = sample_array.copy() #array([0, 1, 2, 3, 4])
a_copy[0] = 9 # #array([9, 1, 2, 3, 4]) the other is unchaged
```

## Array operations
```python
array1 = np.random.randint(1,4, size=(4))
# results array(4,) with int between 1 to 4
# e.g. array([1, 2, 3, 1])
array2 = np.random.randint(7,9, size=(4))
# results array(4,) with int between 7 to 9
# e.g. array([7, 7, 7, 7])

```
**Element-wise Addition of arrays**
```python
addition = array1 + array2
#results array(4,) with element-wise sums
# e.g. array([ 8,  9, 10,  8])
```

**Note Subtraction, multiplication and division works the same**
```python
addition = array1 + array2
#np.add(array1,array2)

subtraction = array1 - array2
#np.subtract(array1,array2)

multiplication = array1 * array2
#np.multiply(array1,array2)

division = array1 / array2
#np.divide(array1,array2)

"""e.g. 
	array1/array2 	results array(4,)
	with element-wise divison
  array([0.14285714, 0.28571429, 0.42857143, 0.14285714])
"""
```

## Working with arrays ARRANGE, LINSPACE,RESHAPE
### Working with ARANGE method
Note: Arange, unlike other methods only accepts start, stop, and increment
i.e. np.arange(start, stop, increment)
*arange(20), arange(0,20) and arange(0,20,1) all give same 20 elements from 0 to 19 by increment of 1.*
**Example:**
np.arange(10) will have 0 as inclusive lower limit but 10 as exclusive upper limit, or mathematically put: **\[0,10)** 
```python
array3 = np.arange(12)
#results array(12,) of incremental figures from 0 to 11
#e.g. array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11])

array3_1 = np.arange(0,20,10) #results [0,10]
array3_2 = np.arange(0,21,10) #results [0,10,20]
```

### Working with LINSPACE method
np.linspace works almost same as np.random.uniform except, the values between start and stop in np.linspace are evenly spaced and not random. i.e. there is a fixed constant increment between numbers.
**Note:** The lower and upper bound of linspace are both inclusive.
e.g. np.linspace(0,20,15) has both 0 and 20 inclusive i.e. \[0,20] instead of \[0,20) where 20 is exclusive.
```python
array4 = np.linspace(0,20,15)
#results array(15,) of evenly spaced values from 0 to 20
"""e.g.
array([ 0.        ,  1.42857143,  2.85714286,  4.28571429,  5.71428571,
        7.14285714,  8.57142857, 10.        , 11.42857143, 12.85714286,
       14.28571429, 15.71428571, 17.14285714, 18.57142857, 20.        ])
"""
#where np.random.uniform(0,20,15) would simply return array(15,)
#of random values between 0 to 20.
np.linspace(0,20) returns array(50,)
#when num is not defined, it defaults to 50
#syntax np.linspace(start,stop,num,endpoint=True)
#by default endpoint makes upper limit exclusive.
```
**_All methods for rounding works, e.g. array2.round(2)_**

### RESHAPING dimension of an array
```python
array5 = np.linspace(10,20,40)
#result array(40,) of values from 10 to 20
"""e.g.
array([10.        , 10.25641026, 10.51282051, 10.76923077, 11.02564103,
       11.28205128, 11.53846154, 11.79487179, 12.05128205, 12.30769231,
       12.56410256, 12.82051282, 13.07692308, 13.33333333, 13.58974359,
       13.84615385, 14.1025641 , 14.35897436, 14.61538462, 14.87179487,
       15.12820513, 15.38461538, 15.64102564, 15.8974359 , 16.15384615,
       16.41025641, 16.66666667, 16.92307692, 17.17948718, 17.43589744,
       17.69230769, 17.94871795, 18.20512821, 18.46153846, 18.71794872,
       18.97435897, 19.23076923, 19.48717949, 19.74358974, 20.        ])
"""
#RESHAPING!!!
array5.reshape(10,4)
#result array(10,4) same size (40)
"""e.g.
array([[10.        , 10.25641026, 10.51282051, 10.76923077],
       [11.02564103, 11.28205128, 11.53846154, 11.79487179],
       [12.05128205, 12.30769231, 12.56410256, 12.82051282],
       [13.07692308, 13.33333333, 13.58974359, 13.84615385],
       [14.1025641 , 14.35897436, 14.61538462, 14.87179487],
       [15.12820513, 15.38461538, 15.64102564, 15.8974359 ],
       [16.15384615, 16.41025641, 16.66666667, 16.92307692],
       [17.17948718, 17.43589744, 17.69230769, 17.94871795],
       [18.20512821, 18.46153846, 18.71794872, 18.97435897],
       [19.23076923, 19.48717949, 19.74358974, 20.        ]])
"""
```
Note: reshape methods gives new shape results without changing its data. To change the data we need to replace the variable with new shape.
```python
a_array = np.arange(10) #produce shape(10,) of 0 to 9
a_array.reshape(10,1) #produce shape (10,1) but no change to a_array
a_array = a_rray.reshape(10,1) #replaces previous shape.
```

## Indexes and slices
### Getting direct values of rows and columns from an array.
```python
array6 = np.random.randint(0,5,size=(4,3))
"""e.g.
array([[1, 0, 4],
       [2, 3, 0],
       [0, 0, 1],
       [2, 0, 1]])
row0 = array6[0] #return 1st row [1,0,4]
#array6[0], array6[0,] and array6[0,:] are the same of shape (3,)

#also array6[0] and array6[0:1], array[0:1,],etc have same values but different shape (1,3) [[1, 0, 4]]

row3 = array6[3] #returns last 4th row [2,0,1]
#array6[3], array6[3,] and array6[3,:] are the same of shape (3,)

#also array6[3] and array6[3:4], array[3:4,], etc, have same element but different shape (3,1)[[2,0,1]]

col0 = array6[:,0] #returns 1st column [1,2,0,2] of shape(4,)
#array6[:,0] and array6[:,0:1] have same elements but different shape (4,1) that is:
array([[1],
       [2],
       [0],
       [2]])

col2 = array6[:,2] #returns last 3rd col. [4,0,1,1] (4,)
#array6[:,2] and array[:,2:3] have same elements but different shape (4,1) that is:
array([[4],
       [0],
       [1],
       [1]])
"""
```

### Changing values of rows and columns
The dimensions for rows and columns must match the new replacements.
```python
array7 = np.random.randint(3,9,(5,4))
#results array(5,4) of values between 3 and 9
"""e.g.
array([[4, 7, 8, 7],
       [6, 5, 3, 6],
       [6, 3, 3, 4],
       [5, 6, 3, 8],
       [4, 6, 7, 3]])
"""
```

#### Replacing row values
```python
array7[0,:] #returns array(4,) first row [4,7,8,7]

newrow = np.random.randint(0,3,4) #returns array(4,) of values between 0 and 3
"""e.g. 
array([2, 0, 0, 1])
"""
array7[0,:] =newrow #replace [4,7,8,7] to [2,0,0,1]
"""e.g. array7 becomes
array([[2, 0, 0, 1],
       [6, 5, 3, 6],
       [6, 3, 3, 4],
       [5, 6, 3, 8],
       [4, 6, 7, 3]])
"""
```
#### Replacing column values
```python
array7[:,0] #returns first column array(5,) [2, 6, 6, 5, 4]
newcolumn = np.random.randint(21,32,5) #returns array(5,) of values between 21 and 32
"""e.g.
array([30, 25, 30, 29, 21])
"""
array7[:,0] = newcolumn # replaces [2,6,6,5,4] with [30,25,30,29,21]
"""e.g. array7 becomes
array([[30,  0,  0,  1],
       [25,  5,  3,  6],
       [30,  3,  3,  4],
       [29,  6,  3,  8],
       [21,  6,  7,  3]])
"""
```

#### Replacing multiple rows
```python
"""e.g. array7=
array([[30,  0,  0,  1],
       [25,  5,  3,  6],
       [30,  3,  3,  4],
       [29,  6,  3,  8],
       [21,  6,  7,  3]])
"""
#Getting first two rows, limits are [0:2)
array7[0:2] #or array7[0:2,] or array7[0:2,:]
"""e.g. answer is array(2,4)
array([[30,  0,  0,  1],
       [25,  5,  3,  6]])
"""
new_rep_array = np.random.randint(41,46,(2,4))
#this returns array(2,4) with values between 41 to 46
"""e.g.
array([[43, 43, 43, 41],
       [43, 41, 43, 41]])
"""
array7[0:2] = new_rep_array
""" replaces
array([[30,  0,  0,  1],
       [25,  5,  3,  6]])
with:
array([[43, 43, 43, 41],
       [43, 41, 43, 41]])
making array7:
array([[43, 43, 43, 41],
       [43, 41, 43, 41],
       [30,  3,  3,  4],
       [29,  6,  3,  8],
       [21,  6,  7,  3]])
"""

#Note: row 4 & 5 would be array7[3:5] of shape(2,4)
# because limit nature is [3,5) or [3,4]
# where 4th row is 3rd increment
# and 5th row is 4th increment.
"""i.e. array7[3:5] is
array([[29,  6,  3,  8],
       [21,  6,  7,  3]])
"""
```

#### Replacing multiple columns

```python
array8 = np.random.randint(63,69,(4,3))
# returns shape (4,3) with values between 63 to 69
"""i.e.
array([[64, 65, 67],
       [64, 66, 65],
       [63, 66, 68],
       [63, 66, 64]])
"""
array8[:,1:3] #returns 2nd & 3rd column shape (4,2)
"""i.e
array([[65, 67],
       [66, 65],
       [66, 68],
       [66, 64]])
"""
new_columns = np.random.randint(11,18,(4,2))
# returns shape (4,2) with integers between 11 and 18
"""i.e
array([[13, 14],
       [17, 15],
       [12, 11],
       [17, 15]])
"""
array8[:,1:3] = new_columns
"""replaces
array([[65, 67],
       [66, 65],
       [66, 68],
       [66, 64]])
with:
array([[13, 14],
       [17, 15],
       [12, 11],
       [17, 15]])
making array8:
array([[64, 13, 14],
       [64, 17, 15],
       [63, 12, 11],
       [63, 17, 15]])
```

### Fetching non-consecutive rows and columns
```python
array10 = np.random.randint(52,59,(6,4))
"""i.e. 
array([[68, 71, 44, 64],
       [51, 73, 63, 68],
       [60, 51, 42, 38],
       [44, 37, 55, 49],
       [53, 41, 42, 58],
       [74, 53, 55, 72]])
"""
```
#### Selecting and repalcing 3rd and 6th row from (6,4) i.e. \[ \[2,5], : ]
```python
row3and4 = array10[[2,5]] 
#same as array10[[2,5],] and array10[[2,5],:]
""" returns 3rd and 6th row of shape(2,4):
array([[60, 51, 42, 38],
       [74, 53, 55, 72]])
"""
rep_array = np.random.randint(0,10,(2,4))
# returns shape (2,4) with elements between 0 and 10
"""i.e.
array([[4, 0, 1, 4],
       [4, 3, 1, 1]])
"""
array10[[2,5]] = rep_array #replaces 3rd and 6th row
"""
array([[68, 71, 44, 64],
       [51, 73, 63, 68],
       [ 4,  0,  1,  4],
       [44, 37, 55, 49],
       [53, 41, 42, 58],
       [ 4,  3,  1,  1]])
"""
```
#### Selecting and replacing 2nd and 4th column from (6,4)
```python
column2and4 = array10[:,[1,3]]
#returns shape(6,2) of 2nd and 4th row
"""i.e
array([[71, 64],
       [73, 68],
       [ 0,  4],
       [37, 49],
       [41, 58],
       [ 3,  1]])
"""
col_rep = np.random.randint(110,200,(6,2))
#returns shape(6,2) with values between 110,200
"""i.e.
array([[131, 190],
       [117, 190],
       [171, 146],
       [182, 135],
       [177, 174],
       [179, 150]])
"""
array10[:,[1,3]] = col_rep #replaces 2nd &3rd row
"""array10 becomes:
array([[ 68, 131,  44, 190],
       [ 51, 117,  63, 190],
       [  4, 171,   1, 146],
       [ 44, 182,  55, 135],
       [ 53, 177,  42, 174],
       [  4, 179,   1, 150]])
"""
```

## Broadcasting and arrays with different shapes
### Addition of scalar to vector
Adding a vector by scalar variable, it essentially does element-wise addition of the scalar value.
```python
array11 = np.random.randint(0,8,(4,3))
#results shape(4,3) of values between 0 and 8 ie [0,8)
"""i.e.
array([[0, 6, 0],
       [5, 1, 4],
       [4, 7, 4],
       [5, 5, 5]])
"""
scalar1 = 10
result = array11 + scalar1
"""result will be element-wise addition:
array([[10, 16, 10],
       [15, 11, 14],
       [14, 17, 14],
       [15, 15, 15]])
"""
#Other possible element-wise operations
# array11*scalar1 or array11/scalar1 or array11-scalar1
```
All scalar operations are the same element-wise as addition.

### Additions of dimensional arrays
Rules for broadcasting arrays
1. Two arrays are compatible when they have the same shape
2. One arrays is a single row/column e.g. shape (n,), (1,n) or (n,1) and the n-row or n-column match the other array (i.e. n must match).
3. One of the array has fewer dimensions than the other and can be stretched.
```python
# Rule 1: Array of (n,n) and (n,n) i.e same shape  
"""
Rule 2: 
Note (n,) behave as (1,n)
e.g. (3,) behave as (1,3)
i.e. [0,1,2] behave as [[0,1,2]]
Now:
  (n,..) always + to (n,1) #row-match e.g. (5,6) &(5,1)
  (..,n) always + to (1,n) #col-match e.g. (9,4) &(1,4)
  (n,1)  always + to (1,n) #n-with-1-match (7,1) &(1,7)

i.e:
 np.arange(0,30).reshape(5,6)+np.arange(0,5).reshape(5,1)
 np.arange(0,36).reshape(9,4)+np.arange(0,4).reshape(1,4)
 np.arange(0,7).reshape(1,7)+np.arange(0,7).reshape(7,1)
"""

```

## Arithmetic operations
### Sum of elements in array
```python
array_2d = np.random.randint(1,10,(5,4))
"""i.e.
array([[7, 1, 8, 9],
       [8, 5, 6, 8],
       [4, 5, 9, 6],
       [4, 4, 8, 7],
       [3, 4, 9, 9]])
"""
np.sum(array_2d,0) #sums up axis=0 or inner axis, ie. cols
"""
array([26, 19, 40, 39])
"""
np.sum(array_2d,1) #sums up axis=1 or outer axis, ie. rows
"""
array([25, 27, 24, 23, 25])
"""

```
## Walrus operator for shorthand variable reference
```python
#Note: quickRefVar in bracket, is an assignment that can be used immediately outside the bracket in the same expression

#Examples:
#This brings 5
( quickRefVar:=np.arange(10) )[ quickRefVar < 5 ]
( quickRefVar:=np.arange(10) )[ quickRefVar[0] ]
```

## Boolean indexing
Boolean indexing is the creation of an array of boolean values, indicating indexes where the condition is true and false, which can be passed as array parameter to filter out values.
**Note:** 
**_np.array(\[1, 2, 3, 4]) <  3_** is not an operator but rather an array, a boolean index array which in this case would be _np.array(\[True, True, False, False])_

These are called boolean array indexes and can be passed into the same array or another to return results.
E.g.: np.array(\[1, 2, 3, 4])\[ **_np.array(\[ 1, 2, 3, 4 ]) < 2_**  ]
### Searching by boolean index
```python
rand_values = np.random.randint(-20,20,30)
"""rand_values:
array([-17, -16,  14,  -7,  17,  11,  12,  -6,  -1,  -1, -10,  12,  -8,
        11,  14, -20,  -2, -18, -16,  -2,  -4,   5,  17,  -5,  -7,  13,
        10,  -9,  15,  -3])
"""
boolean_index = rand_values >=0
"""i.e. boolean_index:
array([False, False,  True, False,  True,  True,  True, False, False,
       False, False,  True, False,  True,  True, False, False, False,
       False, False, False,  True,  True, False, False,  True,  True,
       False,  True, False])
"""
#Since boolean index is just 1s and 0s, np.sum will return total
np.sum(rand_values <0) #Gives values <0

filtered_array = rand_values[boolean_index]
"""i.e. filtered_array:
array([-17, -16,  14,  -7,  17,  11,  12,  -6,  -1,  -1, -10,  12,  -8,
        11,  14, -20,  -2, -18, -16,  -2,  -4,   5,  17,  -5,  -7,  13,
        10,  -9,  15,  -3])
"""
#Boolean index filter shorthand method
rand_values[ rand_values >=0 ]

#Boolean index with multiple truth values
(rand_values>-2) &(rand_values<2)
"""
array([False, False, False, False, False, False, False, False,  True,
        True, False, False, False, False, False, False, False, False,
       False, False, False, False, False, False, False, False, False,
       False, False, False])
"""
rand_values[(rand_values>-21) &(rand_values<2)]
"""
array([-1, -1])
"""
```
### Operations by boolean index
```python
#Boolean index replacement
rand_values[ rand_values >=0 ]=99
rand_values
"""rand_values:
array([-17, -16,  99,  -7,  99,  99,  99,  -6,  -1,  -1, -10,  99,  -8,
        99,  99, -20,  -2, -18, -16,  -2,  -4,  99,  99,  -5,  -7,  99,
        99,  -9,  99,  -3])
"""
```

### Operations on 2D arrays by boolean index
**Return select few values by boolean index**
```python
array_2d = np.random.randint(1,10,(5,4))
"""array_2d
array([[1, 8, 1, 2],
       [1, 4, 9, 8],
       [6, 4, 6, 2],
       [6, 1, 2, 6],
       [4, 6, 6, 7]])
"""
#To return 1st &2nd row by boolean index
bool_row_index = [True, True, False, False, False]
#note: boolean index must match axis length
array_2d[bool_row_index,:]
"""i.e.
array([[1, 8, 1, 2],
       [1, 4, 9, 8]])
"""

#To return 3rd &4th col by bool index
bool_col_index = [False, False, True, True]
#note: boolean  index must match axis length
array_2d[:,bool_col_index]
"""i.e.
array([[1, 2],
       [9, 8],
       [6, 2],
       [2, 6],
       [6, 7]])
"""
```

### Searching rows using row boolean index
It is possible to send in an array of true/false values of which row to bring based on boolean index.
```python
array_2d = np.random.randint(1,10,(5,4))
"""array_2d
array([[1, 8, 1, 2],
       [1, 4, 9, 8],
       [6, 4, 6, 2],
       [6, 1, 2, 6],
       [4, 6, 6, 7]])
"""
#Use sum by axis, to get totals of axis and convert the totals in to a boolean index to search.
#Return totals of rows(axis=1 in 2d array)
#note: axis=0 is the innermost and first axis i.e column in 2d array, and last axis is the outer-most, i.e. axis=1 for 2d array, where axis starts from 0 to 1

array_2d_sum = np.sum(array_2d,axis=1) #results shape(5,)
"""array_sum:
array([12, 22, 18, 15, 23])
"""
#Convert the array into boolean index
bool_row_index = array_2d_sum<22
"""results:
array([ True, False,  True,  True, False])
"""
filtered_sum = array_2d[bool_row_index, ]
"""results:
array([[1, 8, 1, 2],
       [6, 4, 6, 2],
       [6, 1, 2, 6]])
"""
#Shorthand using walrus assignment
( wlr:=np.random.randint(1,10, (5,4)) )[ wlr.sum(axis=1)<22, : ]

#searching columns is simply changing
#the axis=0, and from expr,: to :,expr
( wlr:=np.random.randint(1,10, (5,4)) )[ :, wlr.sum(axis=0)<22 ]
```

## Statistical functions
```python
stat_data = np.random.uniform(11.1,25.7,(5,6)).round(1)
"""results:
array([[17.4, 21.7, 12.6, 13.1, 14.6, 25. ],
       [22.4, 15.8, 17.2, 25.7, 16.5, 16.6],
       [24.8, 24.2, 18. , 14.4, 14.9, 13.8],
       [13.9, 18.8, 20.2, 17.2, 20.9, 21.3],
       [25. , 23.1, 11.2, 17.2, 17.7, 15.5]])
"""
#Getting statistical results
stat_data.mean() #or np.mean(stat_data)
stat_data.median()
stat_data.std()
stat_data.max()

#Note these can be done along an axis
stat_data.mean(axis=0) #columns in 2d-array
stat_data.sum(axis=1) #rows in 2d-array

```

## Matrix operations
Two methods can be used for matrix multiplication and dot product operations
np.dot() and np.matmul()
**Dot-product works on the following**
- For 1-dimension, dot-product is computed
- For 2-dimension, matrix multiplication
- For N-dimension it performs sum product of last axis of the first array and second-to-last of the second array
**Matrix multiplication**
- For 2-dimension it performs matrix multiplication
- For n-dimension it treats arays as stacks of matrices and perform multiplication of last two dimensions.

```python
matrix_a = np.arange(30).reshape(5,6)
"""i.e:
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14],
       [15, 16, 17, 18, 19],
       [20, 21, 22, 23, 24],
       [25, 26, 27, 28, 29]])
"""
matrix_b = np.random.choice([4,8,2,3,1,7],(6,5))
"""i.e:
array([[7, 2, 4, 4, 2],
       [1, 1, 1, 8, 8],
       [7, 3, 3, 4, 7],
       [2, 1, 2, 2, 8],
       [4, 8, 8, 1, 8],
       [1, 8, 1, 1, 3]])
"""
#Dot product requires 1st matrix columns align 2nd matrix rows
#Therefore shape(6,5) aligns shape(5,6)
product = np.dot(matrix_a,matrix_b) #or matrix_a.dot(matrix_b)
"""result:
array([[ 42,  82,  50,  31,  93],
       [174, 220, 164, 151, 309],
       [306, 358, 278, 271, 525],
       [438, 496, 392, 391, 741],
       [570, 634, 506, 511, 957]])
"""
#Note: shape(a,b) . shape(b,c) = shape(a,c)

#

```

### Getting unique values and counts
```python
matrix_b = np.random.choice([4,8,2,3,1,7],(6,5))
"""i.e:
array([[7, 2, 4, 4, 2],
       [1, 1, 1, 8, 8],
       [7, 3, 3, 4, 7],
       [2, 1, 2, 2, 8],
       [4, 8, 8, 1, 8],
       [1, 8, 1, 1, 3]])
unique_values = np.unique(matrix_b)
"""result:
array([1, 2, 3, 4, 7, 8])
"""
#Note: np.unique_counts returns two answers, separated by ,
# hence two variable receiving
unique_values,unique_counts = np.unique_counts(matrix_b)
"""
unique_values
array([1, 2, 3, 4, 7, 8])
unique_counts
array([3, 2, 5, 9, 7, 9])
"""
```

## Converting data types
```python
stat_data = np.random.uniform(11.1,25.7,(5,6)).round(1)
"""results:
array([[17.4, 21.7, 12.6, 13.1, 14.6, 25. ],
       [22.4, 15.8, 17.2, 25.7, 16.5, 16.6],
       [24.8, 24.2, 18. , 14.4, 14.9, 13.8],
       [13.9, 18.8, 20.2, 17.2, 20.9, 21.3],
       [25. , 23.1, 11.2, 17.2, 17.7, 15.5]])
"""
#Check data type
stat_data.dtype #returns dtype('float64')
stat_data.astype('float32') #converts to float32 from abt 15 to7 decimals
```

## Linear algebra computation
```python
#Solving linear algebra with numpy

# A square matrix
A = np.array([[4, 2], [1, 3]])
"""
array([[4, 2],
       [1, 3]])
"""
# The inverse of A
A_inv = np.linalg.inv(A)
"""
array([[ 0.3, -0.2],
       [-0.1,  0.4]])
visibly: A- = 1/(det-A)*adjun-A
1/(12-2) * [[3,-2],
						 [-1 4]]

[3/10,  -2/10], [-1/10, 4/10 ]
"""

# The determinant
det_A = np.linalg.det(A)
np.float64(10.000000000000002)

# Eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(A)
"""
eigenvalues
array([5., 2.])
eigenvectors
array([[ 0.89442719, -0.70710678],
       [ 0.4472136 ,  0.70710678]])
"""

# A linear system solution
"""
i.e A*X= b A is the array [[4,2],[1,3]]
 b is [1,2]
 also expressed as:
 4X1 +2X2     = 1
 1X1 +3X2     = 2
 [4   2] [X1] = [1]
 [1   3] [X2] = [2]
here: Ax=b, makes A=[[4,2],[1,3]] x=[x1,x2] b=[1,2]
"""
A = np.array([[4, 2], [1, 3]])
b = np.array([1, 2])
x = np.linalg.solve(A, b)
"""results of X = [x1,x2] in AX=b
array([-0.1,  0.7])
"""

```

## Handling NotANumber(NaN) and Infinities
```python
#Generating a list with np.nan values
val_mix = np.random.choice([1,3,4,np.nan,5,np.inf],size=(5,3))
"""
array([[nan,  4.,  4.],
       [ 1.,  3.,  4.],
       [nan,  3., inf],
       [nan,  5.,  4.],
       [ 5.,  1., inf]])
"""
#Check for nans by returning boolean index
np.isnan(val_mix)
"""
array([[ True, False, False],
       [False, False, False],
       [ True, False, False],
       [ True, False, False],
       [False, False, False]])
"""
#Return nans only
val_mix[ np.isnan(val_mix) ]
"""
array([nan, nan, nan])
"""
#checking infinities
np.isinf(val_mix)
"""
array([[False, False, False],
       [False, False, False],
       [False, False,  True],
       [False, False, False],
       [False, False,  True]])
"""
#Returning infinities
val_mix[ np.isinf(val_mix)]
"""
array([inf, inf])
"""
#Replacing NaNs and Infs
val_mix
"""
array([[nan,  4.,  4.],
       [ 1.,  3.,  4.],
       [nan,  3., inf],
       [nan,  5.,  4.],
       [ 5.,  1., inf]])
"""
#swaps nan with 0.0, inf with 999 and neginf with -999
np.nan_to_num(val_mix, nan=0.0, posinf=999, neginf=-999)
"""
array([[  0.,   4.,   4.],
       [  1.,   3.,   4.],
       [  0.,   3., 999.],
       [  0.,   5.,   4.],
       [  5.,   1., 999.]])
"""
```

### Placing mix of generated values in single array
```python
log_values = np.log( np.random.randint(-5,5,10) )
"""
array([0.        ,       -inf,       -inf,       -inf,        nan,
       0.        ,       -inf, 0.69314718,        nan, 0.        ])
"""
arange_values = np.arange(10)
"""
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
"""
nan_and_inf = [np.nan, np.inf, -np.inf]
"""
[nan, inf, -inf]
"""
#Concatenation of multiple arrays
concatenated_vals = np.concatenate((log_values,arange_values,nan_and_inf))
"""
array([0.        ,       -inf,       -inf,       -inf,        nan,
       0.        ,       -inf, 0.69314718,        nan, 0.        ,
       0.        , 1.        , 2.        , 3.        , 4.        ,
       5.        , 6.        , 7.        , 8.        , 9.        ,
              nan,        inf,       -inf])
"""
```

### Concatenation of arrays acrros dimensions
**One dimension concatenation**
```python
item_1 = np.arange(3)
#array([0, 1, 2])
item_2 = np.linspace(5,9,5).astype('int')
#array([5, 6, 7, 8, 9])
np.concatenate([item_1,item_2])
#array([0, 1, 2, 5, 6, 7, 8, 9])
```
**Two dimension concatenation**
```python
item_3 = np.arange(4).reshape(2,2)
"""
array([[0, 1],
       [2, 3]])
"""
item_4 = np.arange(6,10).reshape(2,2)
"""
array([[6, 7],
       [8, 9]])
"""
np.concatenate([item_3,item_4])
#same as np.concatenate([item_3,item_4],axis=0)
"""
array([[0, 1],
       [2, 3],
       [6, 7],
       [8, 9]])
"""
np.concatenate([item_3,item_4],1) #same as axis=1
"""
array([[0, 1, 6, 7],
       [2, 3, 8, 9]])
"""

```
