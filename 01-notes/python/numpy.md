#### Create Jupyter Notebook
	Ctrl + Shift + P

## Intro to Numpy
```python
import numpy as np
## CREATE NUMPY ARRAY
numpy_array = np.array([1, 2, 3, 4, 5]) # all elements must be the same type

## MODIFY DATA
print(numpy_array * 10)
```

## Print Array
```python
## Look at the shape of the array
print(matrix_2d.shape) ### rows, columns

## Number of Dimensions
print(matrix_2d.ndim)

## Size of Array
print(matrix_2d.size)

## Data Type of Array
print(matrix_2d.dtype)

## Item Size
print(matrix_2d.itemsize)

## Number of Bytes
print(matrix_2d.nbytes)
```
## Create Arrays
```python
# RANGE
arr = np.arange(0, 10, 2) # start, end, step

# LINSPACE -> arithmetic
arr = np.linspace(0, 1, 5) # start, end, number of elements

# ZEROS AND ONES
zeros = np.zeros(5)
ones = np.ones(5)
	ones = np.ones((2,3,4))

# FULL
full = np.full(5, 7) # shape, fill_value

# IDENTITY
identity = np.eye(3)

# RANDOM
random = np.random.rand(5,3) # truly random
random = np.random.random((5,3))
random = np.random.randint(1, 10, size=5) # with range and size, int32/float32 = 4 bytes, int64/float64 = 8 bytes
```

## Array Dtype
```python
arr = np.array([1, 2, 3, 4, 5])
print({arr.dtype}) #int 64

arr_mixed = np.array([1, 2.5, 3]) # Mixed types -> promoted to float

# SPECIFYING TYPES
arr_mixed = np.array([1, 2, 3], dtype=np.float32)
arr_mixed = arr_mixed.astype(np.float64)
```

## Multi Dimensional Array

```python
## 2 Dimension
matrix_2d = np.array([[1,2,3], [4,5,6], [7,8,9]])

## 3 Dimension
matrix_3d = np.array([[[1,2,3], [3,4,5]], [[5,6,7], [7,8,9]]])
	### Two Pages -> Two Rows -> Three Values
```

## Indexing and Slicing
```python
## Slicing
print(arr[-1])
print(arr[::2]) ### Start Stop End

## Slicing for Multi Dimensional
arr = np.array([[1,2,3], [4,5,6], [7,8,9]])
print(arr[1,2]) ### Row, Column
print(arr[1,:]) ### Row, All the items in Column
print(arr[0:2,0:2])

## Boolean Indexing
print(arr[arr > 5])
print(arr[arr % 2 == 0])
```

## Array Operations
```python
## Element Wise Operations
a = np.array([1,2,3,4,5])
b = np.array([6,7,8,9,10])
print(np.square(a))
print(a + b)

## Scalar Operations
print(a + 10)
print(a ** 3)

## Comparison Operations
print(a > 0) ### [True, True, True, True, True]
```

## Array Manipulation
```python
## Reshape
arr = np.arange(12)
reshaped = arr.reshape(3,4)

## Reshape with -1 (auto-calculate dimensions)
reshaped = arr.reshape(2,-1)

## Flatten
flattened = reshaped.flatten()

## Transpose
array_name.T 

## Concatenation
a = np.array([[1,2,3], [4,5,6]])
b = np.array([[4,5,6], [7,8,9]])

print(np.hstack((a, b)))
print(np.vstack((a, b)))
print(np.column_stack((a, b)))
print(np.concatenate((a, b), axis=0)) ### vertical, down rows
print(np.concatenate((a, b), axis=1)) ### horizontal, across columns
```

## Dimensions and Axis
- **Dimension**: Number of axes (2D=2, 3D=3)
- **Axis**: The dimension in which an operation is performed
- **For 2D arrays**: axis=0 is row (vertical), axis=1 is column (horizontal)
```python
## Sum
arr = np.array([[1,2,3], [4,5,6], [7,8,9]])
print(np.sum(arr, axis=0)) ### [12 15 18]
print(np.sum(arr, axis=1)) ### [ 6 15 24]
```
![[Pasted image 20260514203756.png|222]]

## Statistical Operations
```python
print(np.sum(arr))
print(np.mean(arr))
print(np.median(arr))
print(np.std(arr))
print(np.var(arr))
print(np.min(arr))
print(np.max(arr))
print(np.argmin(arr)) ### Index of Min
print(np.argmax(arr)) ### Index of Max

### All is also applicable to multiple dimensions by specifying the axis, order of operation
```

## Linear Algebra Operations
```python
## Element Wise
	a = np.array([[1,2], [3,4]])
	b = np.array([[6,7], [8,9]])
	print(a * b)

## Dot Products
a = np.array([1,2,3])
b = np.array([4,5,6])
print(np.dot(a, b))

## Matrix Properties
print(np.linalg.det(a)) ### Determinant
print(np.linalg.inv(a)) ### Inverse
print(a.T) ### Transpose

## Eigen Values and Vectors
eigenvals, eigenvecs = np.linalg.eig(a)
print(eigenvals)
print(eigenvecs)
```

## Useful Array Methods
```python
## Sorting
print(np.sort(arr)) ### create a copy
arr.sort() ### in place

## Remove Duplicates / Unique Values
print(np.unique(arr))

## Searching with Condition
print(np.where(arr > 2))
print(arr[np.where(arr > 2)])
```

## Image Processing
```python
## Create Random Image
image = np.random.randint(0, 255, size=(10, 10))
brighter = np.clip(image + 50, 0, 255) # adjustment, min, max
```

## Good to Know Info
## 1D → `(5,)`

- Name: **1‑dimensional array / vector**
- Like: A single row (or single column)
- Example: `[1,2,3,4,5]`

---

## 2D → `(rows, cols)`

- Name: **2‑dimensional array / matrix / table**
- Shape: `(n_rows, n_cols)`
- Example: `(2,5)` = 2 rows, 5 columns

---

## 3D → `(depth, rows, cols)`

- Name: **3‑dimensional array / tensor**
- Also called: **stack of matrices / batches**
- Shape: `(depth, rows, cols)`
- Example: `(2,2,5)` = 2 layers × 2 rows × 5 columns

---

## 4D → `(batch, depth, rows, cols)`

- Name: **4‑dimensional tensor**
- Common in: Images (batch × channels × height × width)
- Shape: `(batch, depth, rows, cols)`
- Example: `(10,3,256,256)` = 10 images, 3 color channels, 256×256 pixels

---

## 5D → `(group, batch, depth, rows, cols)`

- Name: **5‑dimensional tensor**
- Shape: `(group, batch, depth, rows, cols)`

#numpy