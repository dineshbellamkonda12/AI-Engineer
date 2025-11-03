## Data Structures Basics

**Data structures** are ways to organize and store data in your computer so you can use it efficiently[12][14]. Think of them like different types of containers - just as you'd use a box for books and a hanger for clothes, you use different data structures for different types of data[19].

### Common Python Data Structures

**Lists** are ordered collections that can hold any type of data and can be modified[14]. You create them with square brackets: `my_list = [1][2][3][4]`[14]. Lists are perfect when you need to maintain order and frequently add or remove items[12].

**Tuples** are similar to lists but cannot be changed once created (immutable)[14]. You create them with parentheses: `my_tuple = (1, 2, 3)`[14]. Use tuples when you want to ensure data stays constant[12].

**Dictionaries** store data in key-value pairs, like a real dictionary where words (keys) have definitions (values)[12][14]. You create them with curly braces: `my_dict = {"name": "John", "age": 25}`[14]. Dictionaries excel at fast lookups when you know the key[12].

**Sets** are unordered collections of unique items[14]. You create them like: `my_set = {1, 2, 3}`[14]. Sets are ideal for removing duplicates and checking membership[14].

## Big O Notation

**Big O notation** describes how the performance of an algorithm changes as the input size grows[2][5]. It tells you the number of operations an algorithm will make, not the actual speed in seconds[9]. Big O focuses on the worst-case scenario, giving you a guarantee that performance won't be slower than the stated complexity[9].

### Common Time Complexities

**O(1) - Constant Time** means the operation takes the same amount of time regardless of input size[10]. Example: accessing an item in a dictionary by key always takes one step[17][18].

**O(log n) - Logarithmic Time** means the operations grow very slowly as input increases[10]. Example: binary search, where you eliminate half the remaining data with each step[10].

**O(n) - Linear Time** means operations grow proportionally with input size[10]. Example: searching through a list to find a specific item requires checking each element once[9][10].

**O(n²) - Quadratic Time** means operations grow with the square of the input size[4][10]. Example: selection sort with nested loops that compare every item with every other item[4].

**O(2^n) - Exponential Time** means operations double with each addition to input[10]. These algorithms become very slow very quickly[10].

### Calculating Big O

When calculating complexity, follow these simplification rules[8]:

1. Remove constants: `O(4 + 2n)` becomes `O(n)`[8]
2. Keep only the fastest-growing term: `O(n² + n)` becomes `O(n²)`[8]
3. Use different variables for different inputs: if you loop through two different lists, use `O(n + m)`[6][8]

### Practical Example

```python
# O(1) - Constant time
def get_first_item(my_list):
    return my_list[0]  # Always one operation

# O(n) - Linear time
def find_item(my_list, target):
    for item in my_list:  # Checks each item once
        if item == target:
            return True
    return False

# O(n²) - Quadratic time
def print_pairs(my_list):
    for i in my_list:  # First loop
        for j in my_list:  # Nested loop
            print(i, j)
```

Understanding Big O helps you compare algorithms and choose the most efficient solution for your problem, especially when working with large datasets[2][5].

-----

## Arrays in Python

**Arrays** are data structures that store multiple elements of the same type in a contiguous block of memory[5][7]. Think of an array like a parking lot - it's a series of numbered spots lined up side by side, where each spot holds one item[7]. Each spot has an index number starting from 0, so you can quickly find any item by its position[3].

### Arrays vs Lists in Python

In Python, you'll primarily work with **lists**, which Python treats like arrays for most purposes[3]. However, there's an important difference[5][8]:

**Lists** can hold mixed data types: `my_list = [1, "hello", 3.14, True]`[2]. Lists are flexible and convenient for general use[2].

**True arrays** (using the `array` module) must contain elements of the same type for better performance and memory efficiency[8]. For example, all integers or all floats[6].

### Creating and Using Arrays

Here's how to work with lists (the most common approach)[3]:

```python
# Create an array (list)
my_array = [7, 12, 9, 4, 11]

# Access elements by index (starts at 0)
print(my_array[0])  # Output: 7 (first element)
print(my_array[2])  # Output: 9 (third element)

# Get array length
length = len(my_array)  # Output: 5

# Loop through elements
for element in my_array:
    print(element)
```

### Common Array Operations

**Adding elements**[1]:
```python
my_array.append(15)  # Adds 15 to the end
```

**Removing elements**[1]:
```python
my_array.pop(1)  # Removes element at index 1
my_array.remove(9)  # Removes first occurrence of value 9
```

**Accessing elements**[3]:
```python
first = my_array[0]  # First element
last = my_array[-1]  # Last element
```

### Using the Array Module

For performance-critical applications with numeric data, use the `array` module[6][8]:

```python
import array as arr

# Create an integer array
numbers = arr.array('i', [1, 2, 3, 4, 5])
# 'i' means integer type

# Create a float array
decimals = arr.array('f', [1.5, 2.7, 3.9])
# 'f' means float type
```

### Key Characteristics

Arrays have three main features[5]:

1. **Homogeneous**: All elements must be the same data type (in true arrays)[5]
2. **Contiguous**: Elements are stored next to each other in memory[5]
3. **Fixed-size**: Traditional arrays have a predetermined size that cannot easily change[5]

### Performance

Arrays are excellent for **fast lookups** - accessing an element by index takes constant time O(1), meaning it's equally fast whether you have 10 or 10,000 elements[7]. This makes arrays perfect for storing collections where you need quick access to specific positions[7].

------

