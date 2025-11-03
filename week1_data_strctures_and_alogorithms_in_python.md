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


# LINKED LIST 

## Part 1: The Basic Concept

### What is a Linked List? (The Simplest Explanation)

Imagine you have 4 sticky notes with information on them[1][2]:
- Note 1: "Apple"
- Note 2: "Banana"  
- Note 3: "Cherry"
- Note 4: "Date"

**Array way**: You stick all 4 notes in a row on your desk, side by side[1].

**Linked List way**: You place the notes randomly anywhere on your desk, but on each note you write where the next note is located[1][2].

```
Note 1 (on window):        Note 2 (on shelf):
Apple                      Banana
Next → shelf               Next → door

Note 3 (on door):          Note 4 (on chair):
Cherry                     Date
Next → chair               Next → NONE (last one)
```

That's it! A linked list is just data scattered around, with each piece telling you where to find the next piece[3][1].

***

## Part 2: The Two Building Blocks

### Block 1: The Node

A **Node** is like a box with two compartments[2]:

```
┌─────────────────┐
│   DATA          │  ← The actual information you store
├─────────────────┤
│   NEXT          │  ← Address of the next box
└─────────────────┘
```

In Python code:
```python
class Node:
    def __init__(self, data):
        self.data = data    # Compartment 1: your information
        self.next = None    # Compartment 2: address of next node
```

**Example**: Creating one node
```python
# Create a node that stores "Apple"
node1 = Node("Apple")

# What's inside?
node1.data = "Apple"   # The data compartment has "Apple"
node1.next = None      # The next compartment is empty (no connection yet)
```

### Block 2: The Linked List

A **Linked List** only needs to remember ONE thing: where the first node is (called the **HEAD**)[3][2].

```python
class LinkedList:
    def __init__(self):
        self.head = None    # Points to first node (initially empty)
```

**Think of HEAD as**: The starting point of the treasure hunt[2]. You must know where the first clue is, then each clue leads to the next.

***

## Part 3: Building Your First Linked List (Step-by-Step)

### Step 1: Create Individual Nodes

```python
# Create 3 separate nodes
node1 = Node("Apple")
node2 = Node("Banana")
node3 = Node("Cherry")

# Right now they're NOT connected - just 3 separate boxes
```

### Step 2: Connect the Nodes

```python
# Connect them like a chain
node1.next = node2    # Apple's "next" points to Banana
node2.next = node3    # Banana's "next" points to Cherry
node3.next = None     # Cherry is the last one (points to nothing)
```

Visual representation:
```
node1          node2          node3
┌──────┐      ┌──────┐      ┌──────┐
│Apple │ ───→ │Banana│ ───→ │Cherry│ ───→ None
└──────┘      └──────┘      └──────┘
```

### Step 3: Create the Linked List and Set the Head

```python
# Create the linked list
my_list = LinkedList()

# Tell it where the first node is
my_list.head = node1    # Now the list knows to start at "Apple"
```

***

## Part 4: Complete Working Example (Copy This!)

```python
# Step 1: Define Node class
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Step 2: Define LinkedList class
class LinkedList:
    def __init__(self):
        self.head = None
    
    # Method to print the list
    def print_list(self):
        current = self.head              # Start at the first node
        
        while current:                   # While we have a node
            print(current.data, end=' → ')   # Print its data
            current = current.next       # Move to next node
        
        print('None')                    # End of list

# Step 3: Create and use the linked list
my_list = LinkedList()

# Create nodes
node1 = Node("Apple")
node2 = Node("Banana")
node3 = Node("Cherry")

# Connect nodes
node1.next = node2
node2.next = node3

# Set the head
my_list.head = node1

# Print the list
my_list.print_list()
# Output: Apple → Banana → Cherry → None
```

***

## Part 5: Adding New Items (The Magic Part!)

### Adding at the Beginning (FAST - Only 3 Steps!)

```python
def add_at_beginning(self, new_data):
    # Step 1: Create new node
    new_node = Node(new_data)
    
    # Step 2: Make new node point to current head
    new_node.next = self.head
    
    # Step 3: Make new node the new head
    self.head = new_node
```

**Visual example**: Adding "Mango" to the beginning
```
BEFORE:
Head → Apple → Banana → Cherry → None

AFTER:
Head → Mango → Apple → Banana → Cherry → None
         ↓
    (new node points to old head)
```

**Time**: O(1) - Always 3 steps, no matter how long the list is![4][5]

### Adding at the End (SLOWER - Must Walk Through List)

```python
def add_at_end(self, new_data):
    # Step 1: Create new node
    new_node = Node(new_data)
    
    # Step 2: If list is empty, make this the head
    if self.head is None:
        self.head = new_node
        return
    
    # Step 3: Walk to the last node
    last = self.head
    while last.next is not None:    # Keep going until we find the last one
        last = last.next
    
    # Step 4: Connect last node to new node
    last.next = new_node
```

**Visual example**: Adding "Date" to the end
```
Walk through: Head → Apple → Banana → Cherry → None
                                        ↑
                                   (found the last one!)

Connect: Cherry → Date → None
```

**Time**: O(n) - Must walk through all nodes to find the end[5]

***

## Part 6: Array vs Linked List (The Key Differences)

| Question | Array | Linked List |
|----------|-------|-------------|
| **Where are items stored?** | Side-by-side in memory[1] | Scattered anywhere[1] |
| **How do you find items?** | Use index number (position)[1] | Follow the chain from head[1] |
| **Can you jump to item #5?** | YES - instant[1] | NO - must start from #1 and follow links[1] |
| **Adding item at start?** | SLOW - shift everything[1] | FAST - just change 2 pointers[1] |
| **Size fixed?** | YES - decided when created[1] | NO - grow/shrink anytime[1] |
| **Memory usage?** | Less (just stores data)[1] | More (stores data + pointers)[1] |

### Visual Memory Comparison

**Array in memory:**
```
Memory addresses: [100][101][102][103][104]
Array values:     [ 10][ 20][ 30][ 40][ 50]
                    ↑    ↑    ↑    ↑    ↑
              All together in a row!
```

**Linked List in memory:**
```
Memory address 100:   Memory address 305:   Memory address 150:
┌─────┬─────┐        ┌─────┬─────┐        ┌─────┬─────┐
│ 10  │ 305 │ ────→  │ 20  │ 150 │ ────→  │ 30  │None │
└─────┴─────┘        └─────┴─────┘        └─────┴─────┘
  data  next           data  next           data  next
  
Scattered in different places!
```

***

## Part 7: Complete Code with All Operations

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    # Print the list
    def print_list(self):
        if self.head is None:
            print("List is empty")
            return
        
        current = self.head
        while current:
            print(current.data, end=' → ')
            current = current.next
        print('None')
    
    # Add at beginning - FAST O(1)
    def add_at_beginning(self, new_data):
        new_node = Node(new_data)       # Create new node
        new_node.next = self.head       # Point to current head
        self.head = new_node            # Make it the new head
    
    # Add at end - SLOW O(n)
    def add_at_end(self, new_data):
        new_node = Node(new_data)
        
        if self.head is None:           # If list is empty
            self.head = new_node
            return
        
        last = self.head
        while last.next:                # Walk to the end
            last = last.next
        last.next = new_node            # Connect to new node
    
    # Search for a value - O(n)
    def search(self, key):
        current = self.head
        position = 0
        
        while current:
            if current.data == key:
                return f"Found '{key}' at position {position}"
            current = current.next
            position += 1
        
        return f"'{key}' not found in list"
    
    # Delete a node - O(n)
    def delete(self, key):
        current = self.head
        
        # If head has the key
        if current and current.data == key:
            self.head = current.next     # Move head to next node
            return
        
        # Search for the key
        prev = None
        while current and current.data != key:
            prev = current
            current = current.next
        
        # If not found
        if current is None:
            print(f"'{key}' not found")
            return
        
        # Unlink the node
        prev.next = current.next
    
    # Get length - O(n)
    def get_length(self):
        count = 0
        current = self.head
        while current:
            count += 1
            current = current.next
        return count


# ===== USING THE LINKED LIST =====

# Create list
fruits = LinkedList()

# Add items at beginning
print("Adding fruits at beginning:")
fruits.add_at_beginning("Cherry")
fruits.add_at_beginning("Banana")
fruits.add_at_beginning("Apple")
fruits.print_list()
# Output: Apple → Banana → Cherry → None

# Add at end
print("\nAdding 'Date' at end:")
fruits.add_at_end("Date")
fruits.print_list()
# Output: Apple → Banana → Cherry → Date → None

# Search
print("\nSearching:")
print(fruits.search("Banana"))     # Found 'Banana' at position 1
print(fruits.search("Mango"))      # 'Mango' not found in list

# Get length
print(f"\nLength of list: {fruits.get_length()}")  # 4

# Delete
print("\nDeleting 'Banana':")
fruits.delete("Banana")
fruits.print_list()
# Output: Apple → Cherry → Date → None

# Check length again
print(f"New length: {fruits.get_length()}")  # 3
```

***

## Part 8: When to Use What?

### Use ARRAY When:
✅ You need to access items by index quickly (like `list[11]`)[1]
✅ You know the size beforehand[1]
✅ You're reading more than adding/deleting[1]
✅ Memory is limited[1]

**Example**: Storing scores of 100 students (fixed size, access by student number)

### Use LINKED LIST When:
✅ You don't know the size in advance[1]
✅ You're adding/removing items frequently[1]
✅ You always access items in order (first to last)[1]
✅ You're building stacks or queues[1]

**Example**: Music playlist (add songs, remove songs, play in order)

***

## Part 9: Key Points to Remember

1. **Node = Box with 2 compartments**: Data + Pointer to next node[2]

2. **Head = Starting point**: You MUST know where the first node is[3][2]

3. **Last node points to None**: That's how you know it's the end[3]

4. **Fast operations**: Adding/removing at beginning = O(1)[1]

5. **Slow operations**: Finding item, adding at end = O(n)[1]

6. **Arrays = Parking lot** (numbered spots in a row)[1]

7. **Linked Lists = Treasure hunt** (follow clues to find next item)[3]

***

## Part 10: Practice Exercise

Try creating this linked list yourself:
```
1 → 2 → 3 → 4 → None
```

Then:
1. Add 0 at the beginning (should become: `0 → 1 → 2 → 3 → 4 → None`)
2. Add 5 at the end (should become: `0 → 1 → 2 → 3 → 4 → 5 → None`)
3. Delete 3 (should become: `0 → 1 → 2 → 4 → 5 → None`)
4. Print the final list

Use the complete code from Part 7 as reference!

***

