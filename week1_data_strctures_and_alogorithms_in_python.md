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


# Linked List - Complete Study Notes

## What is a Linked List?

A **linked list** is a way to store data where each piece of information (called a **node**) contains two parts[1][2]:
1. The actual data you want to store
2. A pointer (address) that tells you where the next piece of data is located

Think of it like a **scavenger hunt**[2]: Each clue has information AND tells you where to find the next clue. The clues can be anywhere in the city - they don't need to be next to each other[2].

## Visual Comparison: Array vs Linked List

### Array Structure
```
Memory Address:  100   101   102   103   104
Array:          [10] [20] [30] [40] [50]
                  ↑
                Index 0, 1, 2, 3, 4
```
**Key Point**: All elements sit **side-by-side** in memory[3][4]. Like parked cars in a parking lot - all in a row[4].

### Linked List Structure
```
Memory Address:  100         305         150         420
Linked List:    [10|305] → [20|150] → [30|420] → [40|NULL]
                 data next   data next   data next   data next
                   ↑
                 HEAD
```
**Key Point**: Elements can be **anywhere** in memory[3][2]. Each node stores the address of the next node[2]. Like treasure hunt clues scattered across town[2].

## Major Differences: Array vs Linked List

| Feature | Array | Linked List |
|---------|-------|-------------|
| **Memory Storage** | Contiguous (side-by-side)[3][4] | Non-contiguous (scattered)[3][4] |
| **Size** | Fixed size[4][5] | Dynamic (can grow/shrink)[4][5] |
| **Memory Allocation** | Compile time (when program starts)[4][5] | Runtime (as needed)[4][5] |
| **Accessing Elements** | Fast O(1) - direct index access[3][5] | Slow O(n) - must traverse from head[3][5] |
| **Insertion at Beginning** | Slow O(n) - shift all elements[3][5] | Fast O(1) - just update pointers[3][5] |
| **Deletion** | Slow O(n) - shift elements[3][5] | Fast O(1) - update pointers[3][5] |
| **Memory Required** | Less (just data)[4][5] | More (data + pointers)[4][5] |
| **Best For** | Random access, known size | Frequent insertions/deletions[3] |

## Complete Python Code Examples

### Array (List) Implementation

```python
# Creating an array
fruits = ['apple', 'banana', 'cherry', 'date']

# Accessing elements - FAST O(1)
print(fruits[0])      # Output: apple
print(fruits[2])      # Output: cherry

# Inserting at beginning - SLOW O(n)
# All elements must shift right
fruits.insert(0, 'mango')  
# Result: ['mango', 'apple', 'banana', 'cherry', 'date']

# Deleting from middle - SLOW O(n)
# All elements after must shift left
fruits.pop(2)  # Removes 'banana'
# Result: ['mango', 'apple', 'cherry', 'date']

# Memory visualization
# fruits: [100][101][102][103] - all side by side
```

### Linked List Implementation

```python
# Step 1: Define Node class
class Node:
    def __init__(self, data):
        self.data = data      # Stores the actual value
        self.next = None      # Pointer to next node (initially None)

# Step 2: Define LinkedList class
class LinkedList:
    def __init__(self):
        self.head = None      # First node (initially empty)
    
    # Insert at beginning - FAST O(1)
    def insert_at_beginning(self, new_data):
        # Create new node
        new_node = Node(new_data)
        
        # Make new node point to current head
        new_node.next = self.head
        
        # Make new node the new head
        self.head = new_node
    
    # Insert at end - SLOW O(n) because we must traverse
    def insert_at_end(self, new_data):
        new_node = Node(new_data)
        
        # If list is empty, make new node the head
        if self.head is None:
            self.head = new_node
            return
        
        # Traverse to the last node
        last = self.head
        while last.next:
            last = last.next
        
        # Make last node point to new node
        last.next = new_node
    
    # Delete a node - O(n) because we must find it
    def delete_node(self, key):
        # Store head node
        temp = self.head
        
        # If head contains the key
        if temp and temp.data == key:
            self.head = temp.next
            temp = None
            return
        
        # Search for the key
        prev = None
        while temp and temp.data != key:
            prev = temp
            temp = temp.next
        
        # If key not found
        if temp is None:
            return
        
        # Unlink the node
        prev.next = temp.next
        temp = None
    
    # Search for element - SLOW O(n)
    def search(self, key):
        current = self.head
        
        while current:
            if current.data == key:
                return True
            current = current.next
        
        return False
    
    # Print the linked list
    def print_list(self):
        current = self.head
        while current:
            print(current.data, end=' -> ')
            current = current.next
        print('None')
    
    # Get length of list
    def get_length(self):
        count = 0
        current = self.head
        while current:
            count += 1
            current = current.next
        return count

# Using the Linked List
ll = LinkedList()

# Insert elements
ll.insert_at_beginning('cherry')
ll.insert_at_beginning('banana')
ll.insert_at_beginning('apple')

print("Initial list:")
ll.print_list()  
# Output: apple -> banana -> cherry -> None

# Insert at end
ll.insert_at_end('date')
print("\nAfter inserting at end:")
ll.print_list()  
# Output: apple -> banana -> cherry -> date -> None

# Search
print("\nSearching for 'banana':", ll.search('banana'))  # True
print("Searching for 'mango':", ll.search('mango'))    # False

# Delete
ll.delete_node('banana')
print("\nAfter deleting 'banana':")
ll.print_list()  
# Output: apple -> cherry -> date -> None

# Get length
print("\nLength of list:", ll.get_length())  # 3
```

## Why Insertion/Deletion is Faster in Linked Lists

### Array Insertion Example
```python
# Array: [10, 20, 30, 40, 50]
# Insert 15 at position 1

# Step 1: Shift 20 → position 2
# Step 2: Shift 30 → position 3
# Step 3: Shift 40 → position 4
# Step 4: Shift 50 → position 5
# Step 5: Insert 15 at position 1
# Result: [10, 15, 20, 30, 40, 50]
# Time: O(n) - must shift n elements
```

### Linked List Insertion Example
```python
# Linked List: 10 → 20 → 30 → 40 → 50
# Insert 15 between 10 and 20

# Step 1: Create new node with data 15
# Step 2: Make 15 point to 20
# Step 3: Make 10 point to 15
# Result: 10 → 15 → 20 → 30 → 40 → 50
# Time: O(1) - just change 2 pointers (if you have the position)
```

## Real-World Analogy

**Array = Apartment Building**
- All rooms are numbered and in order
- Easy to find room 304 - just go to floor 3
- But if you want to add a room between 304 and 305, you must renumber ALL rooms after it

**Linked List = Treasure Hunt**
- Each clue can be anywhere in the city
- Each clue tells you where the next one is
- To find the 5th clue, you must start at clue 1 and follow the chain
- But adding a new clue between clue 2 and 3 is easy - just change where clue 2 points

## When to Use Each

### Use Array When:
- You know the size in advance[3][5]
- You need fast access to elements by index[3]
- You access elements randomly (e.g., `list[11]`, `list`)[5]
- Memory is limited (arrays use less memory)[4]

### Use Linked List When:
- Size changes frequently[3][5]
- You insert/delete elements often, especially at the beginning[3]
- You don't know the size in advance[3]
- You access elements sequentially (one after another)[5]
- Implementing stacks, queues, or other dynamic structures[3]

## Key Takeaways

1. **Arrays**: Think "numbered parking spots" - everything in order, easy to find, hard to rearrange[4]
2. **Linked Lists**: Think "treasure hunt" - pieces anywhere, must follow clues, easy to add/remove clues[2]
3. **Trade-off**: Arrays = fast access, slow modification. Linked Lists = slow access, fast modification[3][5]
4. **Memory**: Arrays store just data. Linked Lists store data + pointers (more memory)[4]

