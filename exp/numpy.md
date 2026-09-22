অবশ্যই। এই পুরো NumPy code-টা আমি **একটা একটা concept ধরে Banglay**, ছোট example আর **output কীভাবে আসে** সেটা দিয়ে বুঝাচ্ছি। সবচেয়ে গুরুত্বপূর্ণ হলো—শুধু syntax মুখস্থ না করে **NumPy দিয়ে আসলে কী problem solve করা হয়** সেটা বুঝবে।

---

# 0. NumPy আসলে কী?

**NumPy = Numerical Python**

Python-এর normal `list` দিয়ে অনেকগুলো number নিয়ে কাজ করা যায়, কিন্তু NumPy-এর `array` দিয়ে:

* অনেক দ্রুত numerical calculation করা যায়
* একসাথে হাজার/লাখ সংখ্যার উপর operation করা যায়
* matrix/vector নিয়ে কাজ করা সহজ
* data science, ML, AI-তে খুব বেশি ব্যবহৃত হয়

ধরো:

```python
numbers = [1, 2, 3, 4]

```

তুমি যদি প্রত্যেকটার সাথে `10` যোগ করতে চাও, normal Python-এ:

```python
result = [x + 10 for x in numbers]
```

NumPy-তে:

```python
numbers = np.array([1, 2, 3, 4])

result = numbers + 10

print(result)
```

Output:

```text
[11 12 13 14]
```

অর্থাৎ NumPy-এর বড় সুবিধা হলো **একসাথে পুরো array-এর উপর mathematical operation করা যায়।**

---

# 1. NumPy install এবং import

```python
!pip install numpy
```

এটা মূলত Google Colab/Jupyter-এর জন্য।

তারপর:

```python
import numpy as np
```

এখানে:

```text
numpy → library
np    → ছোট নাম/alias
```

তাই পরে:

```python
np.array()
np.zeros()
np.mean()
```

ইত্যাদি লিখতে পারো।

---

# 2. NumPy Array তৈরি করা

## Python list

```python
list1 = [1, 2, 3]

print(list1)
```

Output:

```text
[1, 2, 3]
```

এটা Python-এর সাধারণ list।

এখন এটাকে NumPy array বানাই:

```python
arr = np.array(list1)

print(arr)
```

Output:

```text
[1 2 3]
```

দেখতে প্রায় একই, কিন্তু ভিতরের data structure আলাদা।

```python
print(type(arr))
```

Output:

```text
<class 'numpy.ndarray'>
```

`ndarray` = N-dimensional array.

---

# 3. Dimension বা `ndim`

এটা খুব গুরুত্বপূর্ণ।

```python
arr = np.array([1, 2, 3])

print(arr.ndim)
```

Output:

```text
1
```

কারণ এটা একটা **1D array**।

Visualize করো:

```text
[1 2 3]
```

---

## 2D Array

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

দেখতে:

```text
1 2 3
4 5 6
```

এটা:

```python
print(arr.ndim)
```

→ `2`

কারণ এখানে:

```text
row
 ↓
[1 2 3]
[4 5 6]
```

দুই dimension:

```text
row × column
```

---

## 3D Array

এখানে একটা জিনিস তোমার code-এর comment-এর সাথে একটু confusing।

3D মানে শুধু "৩টা list" না।

ধরো:

```python
arr = np.array([
    [
        [1, 2, 3],
        [4, 5, 6]
    ],

    [
        [7, 8, 9],
        [10, 11, 12]
    ]
])
```

এটা:

```text
Layer 0:

1  2  3
4  5  6


Layer 1:

7   8   9
10 11  12
```

Shape:

```text
(2, 2, 3)
```

মানে:

```text
2 layers
2 rows
3 columns
```

তাই:

```python
arr.ndim
```

→ `3`

---

# 4. Array-এর সবচেয়ে গুরুত্বপূর্ণ ৪টা attribute

ধরো:

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

এখন:

```python
print(arr.shape)
print(arr.size)
print(arr.dtype)
print(arr.ndim)
```

---

## `shape`

```python
arr.shape
```

Output:

```text
(2, 3)
```

মানে:

```text
2 rows
3 columns
```

Visual:

```text
1 2 3
4 5 6
↑ ↑ ↑
3 columns

2 rows
```

3D হলে:

```text
(2, 2, 3)
```

মানে:

```text
2 layers × 2 rows × 3 columns
```

---

## `size`

```python
arr.size
```

Output:

```text
6
```

কারণ মোট element:

```text
1 2 3
4 5 6
```

= 6টা।

---

## `dtype`

```python
arr.dtype
```

যেমন:

```text
int64
```

মানে array-এর element কী ধরনের number।

যেমন:

```python
np.array([1, 2, 3])
```

→ integer

```python
np.array([1.2, 2.5])
```

→ float

---

## `ndim`

```python
arr.ndim
```

কত dimension:

```text
[1,2,3]          → 1D
[[1,2],[3,4]]    → 2D
[[[...]]]        → 3D
```

---

# 5. Array বানানোর shortcut

প্রতিবার manually:

```python
np.array(...)
```

করতে হয় না।

NumPy অনেক ধরনের ready-made array তৈরি করতে পারে।

---

## `np.zeros()`

```python
np.zeros((2, 3))
```

Output:

```text
[[0. 0. 0.]
 [0. 0. 0.]]
```

মানে:

```text
2 rows
3 columns
সব 0
```

---

## `np.ones()`

```python
np.ones((2, 3))
```

Output:

```text
[[1. 1. 1.]
 [1. 1. 1.]]
```

সব `1`।

---

## `np.full()`

```python
np.full((2, 3), 9)
```

Output:

```text
[[9 9 9]
 [9 9 9]]
```

মানে:

> 2×3 matrix বানাও এবং প্রত্যেক জায়গায় 9 বসাও।

---

# 6. Identity Matrix — `np.eye()`

```python
np.eye(3)
```

Output:

```text
1 0 0
0 1 0
0 0 1
```

এটাকে **Identity Matrix** বলে।

Diagonal:

```text
1
  1
    1
```

বাকি সব:

```text
0
```

Linear algebra / ML-এ এটা গুরুত্বপূর্ণ।

---

# 7. `np.empty()`

```python
np.empty(3)
```

এটা 3টা জায়গা তৈরি করে কিন্তু **নিজে থেকে 0 বসানোর guarantee দেয় না**।

যে memory values আগে ছিল সেগুলো দেখা যেতে পারে।

তাই beginner হিসেবে:

```python
np.zeros()
```

আর

```python
np.empty()
```

এক জিনিস ভাববে না।

---

# 8. `np.arange()`

এটা অনেক গুরুত্বপূর্ণ।

```python
np.arange(2, 10, 2)
```

Output:

```text
[2 4 6 8]
```

Syntax:

```python
np.arange(start, stop, step)
```

এখানে:

```text
start = 2
stop  = 10
step  = 2
```

**10 included হবে না।**

আরেকটা:

```python
np.arange(1, 10)
```

Output:

```text
[1 2 3 4 5 6 7 8 9]
```

---

# 9. `np.linspace()`

এটা `arange()` থেকে একটু আলাদা।

```python
np.linspace(1, 10, 4)
```

মানে:

> 1 থেকে 10 পর্যন্ত মোট 4টা equally spaced number দাও।

Output:

```text
[1. 4. 7. 10.]
```

অর্থাৎ এখানে তুমি **কয়টা value চাও** সেটা বলছ।

### Difference

```python
np.arange(1, 10, 2)
```

→ step কী হবে সেটা বলছ।

```python
np.linspace(1, 10, 5)
```

→ মোট কয়টা value চাই সেটা বলছ।

---

# 10. Random Array

## Random float

```python
np.random.rand(2, 3)
```

যেমন:

```text
[[0.34 0.82 0.11]
 [0.56 0.21 0.91]]
```

প্রতিবার different value আসতে পারে।

---

## Random integer

```python
np.random.randint(1, 100, (2, 3))
```

মানে:

```text
1 থেকে 99
2×3 array
```

যেমন:

```text
[[34 71 12]
 [89 44 67]]
```

---

# 11. Indexing

এটা Python list-এর মতোই।

```python
a = np.array([10, 20, 30, 40, 50])
```

Index:

```text
value:  10  20  30  40  50
index:   0   1   2   3   4
```

তাই:

```python
a[0]
```

→ `10`

```python
a[3]
```

→ `40`

শেষ element:

```python
a[-1]
```

→ `50`

---

# 12. Slicing

Syntax:

```python
array[start : stop : step]
```

Important:

> `stop` included হয় না।

ধরো:

```python
a = np.array([10,20,30,40,50])
```

```python
a[0:3]
```

Output:

```text
[10 20 30]
```

কারণ index:

```text
0 → 10
1 → 20
2 → 30
3 → stop
```

---

## শেষ 3টা

```python
a[-3:]
```

→

```text
[30 40 50]
```

---

## Step

```python
a[::2]
```

→

```text
[10 30 50]
```

মানে:

```text
একটা নাও
একটা বাদ দাও
একটা নাও
```

---

# 13. 2D Array indexing

ধরো:

```python
arr = np.array([
    [1,2,3],
    [4,5,6]
])
```

এটা:

```text
       col
       0 1 2
row 0  1 2 3
row 1  4 5 6
```

তাই:

```python
arr[0]
```

→ প্রথম row:

```text
[1 2 3]
```

```python
arr[1]
```

→

```text
[4 5 6]
```

---

## নির্দিষ্ট element

```python
arr[0][1]
```

মানে:

```text
row 0
column 1
```

→ `2`

আরও clean way:

```python
arr[0, 1]
```

→ `2`

আমি তোমাকে NumPy-তে দ্বিতীয়টাই ব্যবহার করতে recommend করব:

```python
arr[row, column]
```

---

# 14. পুরো Column বের করা

এটা NumPy-এর খুব powerful feature।

```python
arr = np.array([
    [1,2,3],
    [4,5,6]
])
```

প্রথম column:

```python
arr[:, 0]
```

Output:

```text
[1 4]
```

এখানে:

```text
:
```

মানে:

> সব row

আর:

```text
0
```

মানে:

> column 0

তাই:

```python
arr[:, 1]
```

→

```text
[2 5]
```

---

# 15. 3D Array বুঝো

3D array নিয়ে শুরুতে confusion হয়।

ভাবো একটা building:

```text
Layer 0
---------
1 2 3
4 5 6

Layer 1
---------
7 8 9
10 11 12
```

Shape:

```text
(2, 2, 3)
```

মানে:

```text
layers = 2
rows   = 2
columns = 3
```

তখন:

```python
arr[0]
```

→ প্রথম layer।

```python
arr[1]
```

→ দ্বিতীয় layer।

আর:

```python
arr[0, 1, 2]
```

মানে:

```text
layer 0
row 1
column 2
```

---

# 16. Reshape

ধরো:

```python
arr = np.array([1,2,3,4,5,6])
```

বর্তমান shape:

```text
(6,)
```

এখন:

```python
arr.reshape(2,3)
```

Output:

```text
[[1 2 3]
 [4 5 6]]
```

মানে 6টা number-কে:

```text
2 rows × 3 columns
```

এ সাজালাম।

---

আর:

```python
arr.reshape(3,2)
```

হলে:

```text
[[1 2]
 [3 4]
 [5 6]]
```

### সবচেয়ে গুরুত্বপূর্ণ rule:

Total elements একই থাকতে হবে।

```text
6 elements
```

তাই:

```text
2 × 3 = 6   ✅
3 × 2 = 6   ✅
6 × 1 = 6   ✅
```

কিন্তু:

```text
4 × 2 = 8   ❌
```

---

# 17. Flatten

ধরো:

```python
arr = np.array([
    [1,2,3],
    [4,5,6]
])
```

এটা 2D।

```python
arr.flatten()
```

Output:

```text
[1 2 3 4 5 6]
```

অর্থাৎ:

> যেকোনো multi-dimensional array → 1D

---

# 18. Stacking

ধরো:

```python
a = np.array([1,2,3])
b = np.array([4,5,6])
```

## `vstack`

```python
np.vstack((a,b))
```

Output:

```text
[[1 2 3]
 [4 5 6]]
```

Vertical:

```text
1 2 3
4 5 6
```

অর্থাৎ row হিসেবে বসালাম।

---

## `hstack`

```python
np.hstack((a,b))
```

Output:

```text
[1 2 3 4 5 6]
```

এক লাইনে পাশাপাশি বসালাম।

---

# 19. Splitting

ধরো:

```python
c = np.array([
    [1,2,3],
    [4,5,6]
])
```

## `hsplit`

```python
np.hsplit(c, 3)
```

Column-wise ভাগ করবে:

```text
[[1]
 [4]]

[[2]
 [5]]

[[3]
 [6]]
```

---

## `vsplit`

```python
np.vsplit(c, 2)
```

Row-wise ভাগ:

```text
[[1 2 3]]

[[4 5 6]]
```

সহজভাবে মনে রাখো:

```text
hstack → horizontal
vstack → vertical

hsplit → column-wise split
vsplit → row-wise split
```

---

# 20. Array-তে Mathematical Operation

এটা NumPy-এর সবচেয়ে important সুবিধাগুলোর একটা।

```python
a = np.array([10,20,40,-30])
```

```python
a + 10
```

Output:

```text
[20 30 50 -20]
```

প্রতিটা element-এর সাথে 10 যোগ হয়েছে।

```python
a * 2
```

→

```text
[20 40 80 -60]
```

এটাকে **vectorized operation** বলতে পারো।

---

# 21. Square / Square root

```python
a = np.array([1,4,9])
```

```python
np.square(a)
```

→

```text
[1 16 81]
```

আর:

```python
np.sqrt(a)
```

→

```text
[1. 2. 3.]
```

---

# 22. দুই Array-এর মধ্যে calculation

```python
a = np.array([1,2,3])
b = np.array([4,5,6])
```

### Addition

```python
np.add(a,b)
```

→

```text
[5 7 9]
```

### Subtraction

```python
np.subtract(a,b)
```

→

```text
[-3 -3 -3]
```

### Multiplication

```python
np.multiply(a,b)
```

→

```text
[4 10 18]
```

মানে:

```text
1×4 = 4
2×5 = 10
3×6 = 18
```

---

# 23. Dot Product

এটা একটু important mathematical concept।

```python
a = np.array([1,2,3])
b = np.array([4,5,6])
```

```python
np.dot(a,b)
```

Calculation:

```text
1×4 + 2×5 + 3×6

= 4 + 10 + 18

= 32
```

Output:

```text
32
```

Machine Learning-এ dot product অনেক গুরুত্বপূর্ণ।

---

# 24. Transpose

ধরো:

```python
a = np.array([
    [1,2,3],
    [4,5,6]
])
```

Shape:

```text
(2,3)
```

মানে:

```text
2 rows
3 columns
```

Transpose:

```python
a.T
```

Output:

```text
[[1 4]
 [2 5]
 [3 6]]
```

Shape:

```text
(3,2)
```

অর্থাৎ:

```text
rows ↔ columns
```

সহজভাবে:

```text
1 2 3       1 4
4 5 6  →    2 5
             3 6
```

---

# 25. Statistical Functions

ধরো:

```python
a = np.array([
    [1,2,3],
    [4,5,6]
])
```

### Sum

```python
np.sum(a)
```

```text
1+2+3+4+5+6 = 21
```

---

### Mean

```python
np.mean(a)
```

মানে average:

```text
21 / 6 = 3.5
```

---

### Median

Numbers:

```text
1 2 3 4 5 6
```

মাঝের দুইটা:

```text
3,4
```

Median:

```text
3.5
```

---

### Standard deviation

```python
np.std(a)
```

এটা data কতটা spread out সেটা measure করে।

এখন formula মুখস্থ করার দরকার নেই। Data science-এ পরে detail বুঝবে।

---

### Min / Max

```python
np.min(a)
```

→ `1`

```python
np.max(a)
```

→ `6`

---

# 26. Array Comparison

```python
a = np.array([1,5,3])
b = np.array([4,5,6])
```

```python
a == b
```

Output:

```text
[False True False]
```

কারণ:

```text
1 == 4 → False
5 == 5 → True
3 == 6 → False
```

---

## পুরো array একই কিনা

```python
np.array_equal(a,b)
```

এটা শুধু একটা answer:

```text
False
```

কারণ পুরো array identical না।

---

# 27. Broadcasting ⭐

এটা NumPy-এর সবচেয়ে গুরুত্বপূর্ণ conceptগুলোর একটা।

ধরো:

```python
a = np.array([1,2,3,4])
```

আর:

```python
b = np.array([10])
```

এখন:

```python
a + b
```

Output:

```text
[11 12 13 14]
```

তুমি কিন্তু manually:

```python
10 + 1
10 + 2
10 + 3
10 + 4
```

করনি।

NumPy internally `10`-কে compatible ধরে নিয়ে operation করেছে।

Conceptually ভাবতে পারো:

```text
[1 2 3 4]
[10 10 10 10]
```

তারপর addition।

---

## Broadcasting-এর real example

```python
matrix = np.array([
    [1,2,3],
    [4,5,6]
])

numbers = np.array([10,20,30])
```

এখন:

```python
matrix + numbers
```

Output:

```text
[1+10  2+20  3+30]
[4+10  5+20  6+30]
```

→

```text
[[11 22 33]
 [14 25 36]]
```

`numbers` এক row, কিন্তু NumPy এটাকে দুই row-এর সাথে compatible করে operation করেছে।

এটাই broadcasting।

---

# 28. `NaN` এবং `inf`

Data science-এ real-world data clean না-ও হতে পারে।

যেমন:

```python
data = np.array([10,20,np.nan,40])
```

`np.nan` মানে:

> Not a Number / missing বা undefined numerical value

Check:

```python
np.isnan(data)
```

Output:

```text
[False False True False]
```

---

## `inf`

```python
np.inf
```

মানে infinity।

যেমন:

```python
[1, 2, np.nan, 4, np.inf]
```

---

## `nan_to_num`

```python
np.nan_to_num(data)
```

এটা `NaN`/infinity-কে finite value দিয়ে replace করতে পারে।

যেমন default behaviour-এ:

```text
nan → 0
+inf → বড় finite value
-inf → বড় negative finite value
```

Data cleaning-এ এটা useful হতে পারে।

---

# 29. NumPy Array Save / Load

ধরো:

```python
arr = np.array([1,0,0,8])
```

এখন:

```python
np.save("my_array.npy", arr)
```

এটা array-কে:

```text
my_array.npy
```

file-এ save করবে।

পরে:

```python
loaded_arr = np.load("my_array.npy")
```

দিয়ে আবার load:

```text
[1 0 0 8]
```

পেতে পারো।

---

# 30. তোমার Homework #1

প্রশ্ন:

> 1 থেকে 25 পর্যন্ত 5×5 matrix বানাও।

প্রথমে:

```python
arr = np.arange(1, 26)
```

পাবে:

```text
[ 1  2  3 ... 25]
```

তারপর:

```python
arr = arr.reshape(5,5)
```

পাবে:

```text
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]
 [11 12 13 14 15]
 [16 17 18 19 20]
 [21 22 23 24 25]]
```

### Last row

```python
arr[-1]
```

→

```text
[21 22 23 24 25]
```

### First column

```python
arr[:,0]
```

→

```text
[ 1  6 11 16 21]
```

### 3×3 submatrix

যেমন মাঝখানের 3×3:

```python
arr[1:4, 1:4]
```

→

```text
[[ 7  8  9]
 [12 13 14]
 [17 18 19]]
```

এখানে:

```python
1:4
```

প্রথমটা row-এর জন্য।

দ্বিতীয়:

```python
1:4
```

column-এর জন্য।

অর্থাৎ:

```python
arr[rows, columns]
```

---

# 31. Homework #2 — Broadcasting

তোমার code-এ:

> shape `(3,1)` matrix-এর সাথে shape `(3,)` multiply করো।

ধরো:

```python
a = np.array([
    [1],
    [2],
    [3]
])
```

Shape:

```text
(3,1)
```

আর:

```python
b = np.array([10,20,30])
```

Shape:

```text
(3,)
```

এখন:

```python
a * b
```

Output:

```text
[[10 20 30]
 [20 40 60]
 [30 60 90]]
```

কারণ NumPy broadcasting করে conceptually:

```text
       10  20  30
1 ×
2 ×
3 ×
```

তাই:

```text
1×10  1×20  1×30
2×10  2×20  2×30
3×10  3×20  3×30
```

---

# এখন পুরো NumPy course-টার Mental Map

 এই code-টা মোটামুটি এভাবে মনে রাখো:

```text
                 NumPy
                   │
       ┌───────────┴───────────┐
       ↓                       ↓
     Array                  Calculation
       │                       │
       ├── Create              ├── + - * /
       ├── Shape               ├── square
       ├── Size                ├── sqrt
       ├── Dimension           ├── dot
       ├── Index               ├── mean
       ├── Slice               ├── sum
       ├── Reshape             ├── min/max
       ├── Flatten             └── std
       ├── Stack
       ├── Split
       └── Broadcast
```

আর সবচেয়ে বেশি মনে রাখার মতো syntax:

```python
# Array
np.array()

# Shape
arr.shape

# Dimension
arr.ndim

# Total elements
arr.size

# Create
np.zeros()
np.ones()
np.full()
np.eye()

# Sequence
np.arange()
np.linspace()

# Random
np.random.rand()
np.random.randint()

# Index / Slice
arr[0]
arr[1:4]
arr[:,0]
arr[0,1]

# Reshape
arr.reshape()

# Flatten
arr.flatten()

# Stack
np.vstack()
np.hstack()

# Split
np.vsplit()
np.hsplit()

# Math
np.add()
np.subtract()
np.multiply()
np.divide()
np.square()
np.sqrt()

# Statistics
np.sum()
np.mean()
np.median()
np.std()
np.min()
np.max()

# Compare
np.array_equal()

# Special values
np.isnan()
np.nan_to_num()

# Save/load
np.save()
np.load()
```

প্রথমে এগুলো solid করো:

**1. `np.array()`**
**2. `shape / ndim / size`**
**3. Indexing + slicing**
**4. 2D array `[row, column]`**
**5. `reshape()`**
**6. Array-এর উপর mathematical operation**
**7. `mean/sum/min/max`**
**8. Broadcasting**

বিশেষ করে **`shape` + indexing + slicing + reshape + broadcasting** বুঝে গেলে পরের **Pandas/Matplotlib/ML** শেখা অনেক সহজ হবে।
