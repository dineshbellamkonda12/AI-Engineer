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


----------------


# HASH TABLE - SUPER SIMPLE STUDY NOTES

## Part 1: What is a Hash Table?

A **hash table** (also called a **dictionary** or **hash map**) is a data structure that stores information in **key-value pairs**. Think of it like a real dictionary where you look up a word (key) to find its definition (value).

**Real-world analogy**: A library with a magical system. Instead of searching through every book, you tell the librarian a book title, and they instantly know which shelf to go to. The "magic" that converts the title to a shelf number is called a **hash function**.

In Python, the built-in **dictionary** is actually a hash table!

***

## Part 2: How Hash Tables Work (Simple Explanation)

### The Basic Concept

Imagine you have a storage area with 10 boxes numbered 0 to 9:

```
Box:  [0] [1] [2] [3] [4] [5] [6] [7] [8] [9]
```

You want to store phone numbers with names. Instead of searching through all boxes, you use a **magic formula** (hash function) that converts each name into a box number.

**Example**:
- "Alice" → Magic formula → Box 2
- "Bob" → Magic formula → Box 7
- "Charlie" → Magic formula → Box 4

Now when you need Alice's phone number, you run "Alice" through the formula, get Box 2, and instantly find her number!

***

## Part 3: The Three Key Components

### Component 1: The Key
The **key** is the unique identifier you use to look up data (like a person's name).

### Component 2: The Value
The **value** is the actual data you want to store (like a phone number).

### Component 3: The Hash Function
The **hash function** is a formula that converts a key into an index number (box number).

```
Key → Hash Function → Index → Value

"Alice" → hash("Alice") → 2 → "555-1234"
```

***

## Part 4: Visual Example

### Traditional Array Search (Slow)
```
Finding Bob's phone number:
boxes: ["Alice:555-1234", "Carol:555-5678", "Bob:555-9012", "Dave:555-3456"]
        Check [0]? No     Check [1]? No     Check [2]? YES! Found Bob

Time: O(n) - might check every box
```

### Hash Table Search (Fast)
```
Finding Bob's phone number:
1. Run hash function: hash("Bob") = 7
2. Go directly to box 7
3. Get value: "555-9012"

Time: O(1) - go straight to the right box!
```

***

## Part 5: Simple Python Dictionary (Hash Table)

Python dictionaries ARE hash tables! Here's how to use them:

```python
# Create an empty hash table (dictionary)
phone_book = {}

# Add key-value pairs
phone_book["Alice"] = "555-1234"
phone_book["Bob"] = "555-5678"
phone_book["Charlie"] = "555-9012"

# Look up a value - SUPER FAST O(1)
print(phone_book["Alice"])    # Output: 555-1234
print(phone_book["Bob"])      # Output: 555-5678

# Check if a key exists
if "Alice" in phone_book:
    print("Alice is in the phone book!")

# Update a value
phone_book["Alice"] = "555-9999"

# Delete a key-value pair
del phone_book["Charlie"]

# Print all keys
print(phone_book.keys())      # Output: dict_keys(['Alice', 'Bob'])

# Print all values
print(phone_book.values())    # Output: dict_values(['555-9999', '555-5678'])

# Print all key-value pairs
for name, number in phone_book.items():
    print(f"{name}: {number}")
```

***

## Part 6: How Hash Functions Work (Behind the Scenes)

A hash function converts any key into a number (index).

### Simple Example of a Hash Function

```python
def simple_hash(key, table_size):
    # Convert key to a number
    total = 0
    for char in key:
        total += ord(char)  # ord() gives ASCII value of character
    
    # Use modulo to fit within table size
    index = total % table_size
    return index

# Example
table_size = 10

print(simple_hash("Alice", table_size))    # Might output: 2
print(simple_hash("Bob", table_size))      # Might output: 7
print(simple_hash("Charlie", table_size))  # Might output: 4
```

**How it works**:
1. "Alice" = A(65) + l(108) + i(105) + c(99) + e(101) = 478
2. 478 % 10 = 8 (index 8)
3. Store Alice's data at box 8

***

## Part 7: The Collision Problem

### What is a Collision?

A **collision** happens when two different keys produce the same index.

```
hash("Alice") = 2
hash("Eva") = 2    ← OH NO! Both go to box 2!
```

### Solution: Chaining

**Chaining** means each box can hold multiple items using a list or linked list.

```
Box 0: empty
Box 1: empty
Box 2: ["Alice:555-1234"] → ["Eva:555-7890"]  ← Both stored here!
Box 3: ["Bob:555-5678"]
Box 4: empty
```

Visual representation:
```
Box 2: ┌──────────────┐     ┌──────────────┐
       │ Alice        │  →  │ Eva          │  →  None
       │ 555-1234     │     │ 555-7890     │
       └──────────────┘     └──────────────┘
```

When you search for "Eva":
1. Hash "Eva" → get index 2
2. Go to box 2
3. Search through the chain to find "Eva"

***

## Part 8: Building a Simple Hash Table from Scratch

```python
class HashTable:
    def __init__(self, size=10):
        self.size = size
        # Create array of empty lists (for chaining)
        self.table = [[] for _ in range(self.size)]
    
    # Hash function
    def _hash(self, key):
        total = 0
        for char in str(key):
            total += ord(char)
        return total % self.size
    
    # Insert key-value pair
    def insert(self, key, value):
        index = self._hash(key)
        
        # Check if key already exists
        for i, (k, v) in enumerate(self.table[index]):
            if k == key:
                self.table[index][i] = (key, value)  # Update value
                return
        
        # Key doesn't exist, add it
        self.table[index].append((key, value))
    
    # Search for a key
    def search(self, key):
        index = self._hash(key)
        
        # Search through the chain at this index
        for k, v in self.table[index]:
            if k == key:
                return v
        
        return None  # Key not found
    
    # Delete a key
    def delete(self, key):
        index = self._hash(key)
        
        # Find and remove the key
        for i, (k, v) in enumerate(self.table[index]):
            if k == key:
                del self.table[index][i]
                return True
        
        return False  # Key not found
    
    # Print the hash table
    def display(self):
        for i, bucket in enumerate(self.table):
            print(f"Box {i}: {bucket}")


# ===== USING THE HASH TABLE =====

# Create hash table
ht = HashTable(size=10)

# Insert items
print("Inserting items:")
ht.insert("Alice", "555-1234")
ht.insert("Bob", "555-5678")
ht.insert("Charlie", "555-9012")
ht.insert("Diana", "555-3456")

# Display the table
print("\nHash Table Contents:")
ht.display()

# Search for items
print("\nSearching:")
print(f"Alice's number: {ht.search('Alice')}")
print(f"Bob's number: {ht.search('Bob')}")
print(f"Eve's number: {ht.search('Eve')}")  # Not in table

# Update a value
print("\nUpdating Alice's number:")
ht.insert("Alice", "555-9999")
print(f"Alice's new number: {ht.search('Alice')}")

# Delete an item
print("\nDeleting Charlie:")
ht.delete("Charlie")
print(f"Charlie's number: {ht.search('Charlie')}")  # None

# Display final table
print("\nFinal Hash Table:")
ht.display()
```

**Output Example**:
```
Inserting items:

Hash Table Contents:
Box 0: []
Box 1: [('Bob', '555-5678')]
Box 2: [('Alice', '555-1234'), ('Diana', '555-3456')]
Box 3: [('Charlie', '555-9012')]
Box 4: []
...

Searching:
Alice's number: 555-1234
Bob's number: 555-5678
Eve's number: None
```

***

## Part 9: Python Dictionary Operations

```python
# Creating dictionaries
student_grades = {
    "Alice": 95,
    "Bob": 87,
    "Charlie": 92
}

# Alternative creation
student_ages = dict(Alice=20, Bob=21, Charlie=19)

# Access value
print(student_grades["Alice"])  # 95

# Safe access (returns None if key doesn't exist)
print(student_grades.get("Diana"))  # None
print(student_grades.get("Diana", "Not Found"))  # "Not Found"

# Add new item
student_grades["Diana"] = 88

# Update value
student_grades["Alice"] = 98

# Check if key exists
if "Bob" in student_grades:
    print("Bob is in the dictionary")

# Get all keys
print(student_grades.keys())    # dict_keys(['Alice', 'Bob', 'Charlie', 'Diana'])

# Get all values
print(student_grades.values())  # dict_values([98, 87, 92, 88])

# Get all items
print(student_grades.items())   # dict_items([('Alice', 98), ('Bob', 87), ...])

# Loop through dictionary
for name, grade in student_grades.items():
    print(f"{name}: {grade}")

# Delete an item
del student_grades["Charlie"]

# Remove and return value
grade = student_grades.pop("Bob")  # Returns 87 and removes Bob

# Clear all items
student_grades.clear()

# Get number of items
print(len(student_grades))
```

***

## Part 10: Comparison - Array vs Hash Table

| Operation | Array/List | Hash Table |
|-----------|------------|------------|
| **Search** | O(n) - check each item | O(1) - go directly to index |
| **Insert** | O(1) at end, O(n) at start | O(1) - calculate index and insert |
| **Delete** | O(n) - find then shift items | O(1) - calculate index and delete |
| **Access by index** | O(1) - `list[5]` | Not possible |
| **Ordered?** | YES - maintains order | NO - order not guaranteed |
| **Best for** | Sequential access, ordered data | Fast lookups by key |

### Visual Comparison

**Array - Finding "Bob"**:
```
["Alice", "Charlie", "Diana", "Bob"]
   ↓        ↓         ↓        ↓
Check 1   Check 2   Check 3  Found! (4 steps)
```

**Hash Table - Finding "Bob"**:
```
hash("Bob") = 7
boxes[7] = "Bob's data"
Found! (1 step)
```

***

## Part 11: Real-World Uses

### Use Case 1: Counting Occurrences
```python
# Count word frequency
text = "apple banana apple cherry banana apple"
words = text.split()

word_count = {}
for word in words:
    if word in word_count:
        word_count[word] += 1
    else:
        word_count[word] = 1

print(word_count)
# Output: {'apple': 3, 'banana': 2, 'cherry': 1}
```

### Use Case 2: Caching (Storing Results)
```python
# Store expensive calculations
cache = {}

def expensive_calculation(n):
    if n in cache:
        print("Returning cached result")
        return cache[n]
    
    print("Calculating...")
    result = n * n  # Pretend this is slow
    cache[n] = result
    return result

print(expensive_calculation(5))  # Calculating... 25
print(expensive_calculation(5))  # Returning cached result 25
```

### Use Case 3: Database-like Lookups
```python
# Student database
students = {
    "S001": {"name": "Alice", "age": 20, "grade": "A"},
    "S002": {"name": "Bob", "age": 21, "grade": "B"},
    "S003": {"name": "Charlie", "age": 19, "grade": "A"}
}

# Instant lookup
student_id = "S002"
print(students[student_id]["name"])  # Bob
```

***

## Part 12: Key Points to Remember

1. **Hash Table = Dictionary in Python** - Use `{}` or `dict()`

2. **Key-Value Pairs** - Store data with unique keys for instant lookup

3. **Hash Function** - Converts keys to index numbers (happens automatically in Python)

4. **Speed** - O(1) for search, insert, delete (super fast!)

5. **Collisions** - When two keys map to same index (solved with chaining)

6. **Trade-off** - Uses more memory for faster speed

7. **No Order** - Items are not stored in any particular order

8. **Unique Keys** - Each key can appear only once (values can repeat)

***

## Part 13: When to Use Hash Tables

### Use Hash Table When:
✅ You need fast lookups by key  
✅ You're storing key-value pairs  
✅ Order doesn't matter  
✅ Keys are unique  
✅ Working with large datasets  

**Examples**: Phone books, caching, databases, counting occurrences

### Use Array/List When:
✅ You need to access items by numeric index  
✅ Order matters  
✅ You need to sort items  
✅ You're iterating through all items  

**Examples**: Ordered lists, sequences, stacks, queues

***

## Part 14: Practice Exercise

Try this yourself:

```python
# Create a grade book
grade_book = {}

# Add 5 students with grades
# Search for a specific student
# Update a student's grade
# Delete a student
# Print all students with their grades
# Count how many students have grade 'A'
```

**Solution**:
```python
# Create grade book
grade_book = {
    "Alice": "A",
    "Bob": "B",
    "Charlie": "A",
    "Diana": "C",
    "Eve": "B"
}

# Search
print(grade_book["Alice"])  # A

# Update
grade_book["Bob"] = "A"

# Delete
del grade_book["Diana"]

# Print all
for name, grade in grade_book.items():
    print(f"{name}: {grade}")

# Count A's
a_count = sum(1 for grade in grade_book.values() if grade == "A")
print(f"Students with A: {a_count}")  # 3
```

***

-----------------------


# STACK AND QUEUE - SUPER SIMPLE STUDY NOTES

## PART A: STACK

## Part 1: What is a Stack?

A **stack** is a data structure where elements are arranged vertically, like a stack of plates. You can only add or remove items from the **top**.

**Key Rule: LIFO (Last In, First Out)** - The last item you put in is the first one you take out.

### Real-World Analogies

1. **Stack of Plates**: You add plates on top and take plates from the top. You can't pull a plate from the middle or bottom.

2. **Stack of Books**: The last book you place on the pile is the first one you'll pick up.

3. **Undo Button**: The most recent action is the first one to be undone.

4. **Browser Back Button**: The last page you visited is the first one you go back to.

***

## Part 2: Stack Operations

### The Three Main Operations

1. **Push** - Add an element to the top
2. **Pop** - Remove and return the top element
3. **Peek (or Top)** - Look at the top element without removing it

### Visual Example

```
Initial Stack:        After Push(4):       After Pop():
                      
     [Empty]              [4] ← Top           [Empty]
                          
Push(1):              Push(5):             Push(6):
     [1] ← Top            [5] ← Top           [6] ← Top
                          [4]                 [4]
Push(2):                  
     [2] ← Top        Pop() returns 5:     Peek() returns 6:
     [1]                  [4] ← Top           [6] ← Top
                                              [4]
Push(3):              
     [3] ← Top
     [2]
     [1]
```

***

## Part 3: Simple Stack Using Python List

Python lists can act as stacks using `append()` and `pop()`:

```python
# Create an empty stack
stack = []

# Push elements (add to top)
stack.append(10)    # Stack: [10]
stack.append(20)    # Stack: [10, 20]
stack.append(30)    # Stack: [10, 20, 30]

print("Stack:", stack)  # [10, 20, 30]

# Peek (look at top without removing)
top = stack[-1]
print("Top element:", top)  # 30

# Pop elements (remove from top)
removed = stack.pop()   # Returns 30, Stack: [10, 20]
print("Removed:", removed)

removed = stack.pop()   # Returns 20, Stack: [10]
print("Removed:", removed)

# Check if empty
is_empty = len(stack) == 0
print("Is empty?", is_empty)  # False

# Get size
size = len(stack)
print("Size:", size)  # 1
```

***

## Part 4: Building a Stack Class from Scratch

```python
class Stack:
    def __init__(self):
        self.items = []
    
    # Push - Add element to top
    def push(self, item):
        self.items.append(item)
        print(f"Pushed {item}")
    
    # Pop - Remove and return top element
    def pop(self):
        if self.is_empty():
            return "Stack is empty!"
        return self.items.pop()
    
    # Peek - View top element without removing
    def peek(self):
        if self.is_empty():
            return "Stack is empty!"
        return self.items[-1]
    
    # Check if stack is empty
    def is_empty(self):
        return len(self.items) == 0
    
    # Get size of stack
    def size(self):
        return len(self.items)
    
    # Display stack
    def display(self):
        if self.is_empty():
            print("Stack is empty")
        else:
            print("Stack (top to bottom):")
            for i in range(len(self.items) - 1, -1, -1):
                if i == len(self.items) - 1:
                    print(f"  [{self.items[i]}] ← Top")
                else:
                    print(f"  [{self.items[i]}]")


# ===== USING THE STACK =====

# Create stack
stack = Stack()

# Push elements
stack.push(10)
stack.push(20)
stack.push(30)
stack.push(40)

# Display
stack.display()
# Output:
#   [40] ← Top
#   [30]
#   [20]
#   [10]

# Peek at top
print(f"\nTop element: {stack.peek()}")  # 40

# Pop elements
print(f"\nPopped: {stack.pop()}")  # 40
print(f"Popped: {stack.pop()}")    # 30

# Display again
stack.display()
# Output:
#   [20] ← Top
#   [10]

# Check size
print(f"\nStack size: {stack.size()}")  # 2

# Check if empty
print(f"Is empty? {stack.is_empty()}")  # False
```

***

## Part 5: Stack Time Complexity

| Operation | Time Complexity |
|-----------|----------------|
| Push | O(1) - constant |
| Pop | O(1) - constant |
| Peek | O(1) - constant |
| Search | O(n) - must check all |
| Is Empty | O(1) - constant |

All main operations are **super fast** O(1)!

***

## Part 6: Real-World Stack Applications

### Application 1: Undo Mechanism

```python
class TextEditor:
    def __init__(self):
        self.text = ""
        self.history = Stack()
    
    def type(self, new_text):
        self.history.push(self.text)  # Save current state
        self.text += new_text
        print(f"Text: {self.text}")
    
    def undo(self):
        if not self.history.is_empty():
            self.text = self.history.pop()  # Restore previous state
            print(f"After undo: {self.text}")
        else:
            print("Nothing to undo")

# Use it
editor = TextEditor()
editor.type("Hello")       # Text: Hello
editor.type(" World")      # Text: Hello World
editor.type("!")           # Text: Hello World!
editor.undo()              # After undo: Hello World
editor.undo()              # After undo: Hello
```

### Application 2: Reversing a String

```python
def reverse_string(text):
    stack = []
    
    # Push all characters
    for char in text:
        stack.append(char)
    
    # Pop all characters (LIFO gives reverse order)
    reversed_text = ""
    while stack:
        reversed_text += stack.pop()
    
    return reversed_text

print(reverse_string("hello"))  # Output: olleh
```

### Application 3: Balanced Parentheses Checker

```python
def is_balanced(expression):
    stack = []
    opening = "({["
    closing = ")}]"
    matches = {')': '(', '}': '{', ']': '['}
    
    for char in expression:
        if char in opening:
            stack.append(char)  # Push opening brackets
        elif char in closing:
            if not stack or stack[-1] != matches[char]:
                return False
            stack.pop()  # Pop matching opening bracket
    
    return len(stack) == 0  # Stack should be empty

print(is_balanced("(a + b)"))        # True
print(is_balanced("{[a + b]}"))      # True
print(is_balanced("(a + b]"))        # False
print(is_balanced("{a + b"))         # False
```

***

## PART B: QUEUE

## Part 7: What is a Queue?

A **queue** is a data structure where elements are arranged in a line, like people waiting in line. You add items at the **back** and remove items from the **front**.

**Key Rule: FIFO (First In, First Out)** - The first item you put in is the first one you take out.

### Real-World Analogies

1. **Line at a Store**: First person in line is the first to be served.

2. **Print Queue**: First document sent to printer is printed first.

3. **Call Center**: First caller in queue is the first to be answered.

4. **Airport Security**: First person in line is the first to go through.

***

## Part 8: Queue Operations

### The Three Main Operations

1. **Enqueue (or Push)** - Add an element to the back (rear)
2. **Dequeue (or Pop)** - Remove and return the front element
3. **Peek (or Front)** - Look at the front element without removing it

### Visual Example

```
Initial Queue:            After Enqueue(1):        After Enqueue(2):
[Empty]                   Front → [1] ← Rear       Front → [1, 2] ← Rear

After Enqueue(3):         After Dequeue():         After Enqueue(4):
Front → [1, 2, 3] ← Rear  Front → [2, 3] ← Rear   Front → [2, 3, 4] ← Rear
                          (removed 1)

Step-by-step visualization:

Enqueue(10):  Front → [10] ← Rear
Enqueue(20):  Front → [10, 20] ← Rear
Enqueue(30):  Front → [10, 20, 30] ← Rear
Dequeue():    Front → [20, 30] ← Rear (removed 10)
Peek():       Returns 20 (doesn't remove)
```

***

## Part 9: Simple Queue Using Python List

```python
# Create an empty queue
queue = []

# Enqueue (add to back)
queue.append(10)     # Queue: [10]
queue.append(20)     # Queue: [10, 20]
queue.append(30)     # Queue: [10, 20, 30]

print("Queue:", queue)  # [10, 20, 30]

# Peek at front
front = queue[0]
print("Front element:", front)  # 10

# Dequeue (remove from front)
removed = queue.pop(0)   # Returns 10, Queue: [20, 30]
print("Removed:", removed)

removed = queue.pop(0)   # Returns 20, Queue: [30]
print("Removed:", removed)

# Check if empty
is_empty = len(queue) == 0
print("Is empty?", is_empty)  # False

# Get size
size = len(queue)
print("Size:", size)  # 1
```

***

## Part 10: Building a Queue Class from Scratch

```python
class Queue:
    def __init__(self):
        self.items = []
    
    # Enqueue - Add element to rear
    def enqueue(self, item):
        self.items.append(item)
        print(f"Enqueued {item}")
    
    # Dequeue - Remove and return front element
    def dequeue(self):
        if self.is_empty():
            return "Queue is empty!"
        return self.items.pop(0)
    
    # Peek - View front element without removing
    def peek(self):
        if self.is_empty():
            return "Queue is empty!"
        return self.items[0]
    
    # Check if queue is empty
    def is_empty(self):
        return len(self.items) == 0
    
    # Get size of queue
    def size(self):
        return len(self.items)
    
    # Display queue
    def display(self):
        if self.is_empty():
            print("Queue is empty")
        else:
            print("Queue (front to rear):")
            print(f"  Front → {self.items} ← Rear")


# ===== USING THE QUEUE =====

# Create queue
queue = Queue()

# Enqueue elements
queue.enqueue(10)
queue.enqueue(20)
queue.enqueue(30)
queue.enqueue(40)

# Display
queue.display()
# Output: Front → [10, 20, 30, 40] ← Rear

# Peek at front
print(f"\nFront element: {queue.peek()}")  # 10

# Dequeue elements
print(f"\nDequeued: {queue.dequeue()}")  # 10
print(f"Dequeued: {queue.dequeue()}")    # 20

# Display again
queue.display()
# Output: Front → [30, 40] ← Rear

# Check size
print(f"\nQueue size: {queue.size()}")  # 2

# Check if empty
print(f"Is empty? {queue.is_empty()}")  # False
```

***

## Part 11: Queue Time Complexity

| Operation | Time Complexity |
|-----------|----------------|
| Enqueue | O(1) - constant |
| Dequeue | O(n) - must shift all elements |
| Peek | O(1) - constant |
| Search | O(n) - must check all |
| Is Empty | O(1) - constant |

**Note**: Dequeue is O(n) with simple list implementation because all elements must shift left. Better implementations use circular queues or deque.

***

## Part 12: Better Queue Using `collections.deque`

Python's `collections.deque` (double-ended queue) is optimized for fast operations at both ends:

```python
from collections import deque

# Create queue
queue = deque()

# Enqueue - O(1)
queue.append(10)
queue.append(20)
queue.append(30)

print("Queue:", list(queue))  # [10, 20, 30]

# Dequeue - O(1) with deque!
removed = queue.popleft()  # Returns 10
print("Dequeued:", removed)

# Peek
front = queue[0]
print("Front:", front)  # 20

# Size
print("Size:", len(queue))  # 2
```

***

## Part 13: Real-World Queue Applications

### Application 1: Print Queue

```python
class PrintQueue:
    def __init__(self):
        self.queue = Queue()
    
    def add_document(self, doc_name):
        self.queue.enqueue(doc_name)
        print(f"Added '{doc_name}' to print queue")
    
    def print_next(self):
        if not self.queue.is_empty():
            doc = self.queue.dequeue()
            print(f"Printing: {doc}")
        else:
            print("No documents to print")
    
    def show_queue(self):
        self.queue.display()

# Use it
printer = PrintQueue()
printer.add_document("Report.pdf")
printer.add_document("Invoice.pdf")
printer.add_document("Letter.pdf")
printer.show_queue()
# Output: Front → ['Report.pdf', 'Invoice.pdf', 'Letter.pdf'] ← Rear

printer.print_next()  # Printing: Report.pdf
printer.print_next()  # Printing: Invoice.pdf
```

### Application 2: Customer Service Queue

```python
class CustomerService:
    def __init__(self):
        self.queue = []
    
    def add_customer(self, name):
        self.queue.append(name)
        position = len(self.queue)
        print(f"{name} joined the queue. Position: {position}")
    
    def serve_next(self):
        if self.queue:
            customer = self.queue.pop(0)
            print(f"Now serving: {customer}")
            print(f"Customers waiting: {len(self.queue)}")
        else:
            print("No customers waiting")
    
    def show_queue(self):
        if self.queue:
            print(f"Waiting: {', '.join(self.queue)}")
        else:
            print("Queue is empty")

# Use it
service = CustomerService()
service.add_customer("Alice")   # Position: 1
service.add_customer("Bob")     # Position: 2
service.add_customer("Charlie") # Position: 3
service.show_queue()            # Waiting: Alice, Bob, Charlie
service.serve_next()            # Now serving: Alice
service.serve_next()            # Now serving: Bob
```

***

## Part 14: Stack vs Queue Comparison

| Aspect | Stack | Queue |
|--------|-------|-------|
| **Principle** | LIFO (Last In, First Out) | FIFO (First In, First Out) |
| **Add Location** | Top | Rear (back) |
| **Remove Location** | Top | Front |
| **Analogy** | Stack of plates | Line at a store |
| **Operations** | Push, Pop, Peek | Enqueue, Dequeue, Peek |
| **Use Cases** | Undo, function calls, backtracking | Task scheduling, print queue |

### Visual Comparison

**Stack (LIFO)**:
```
Push 1:    [1]
Push 2:    [2, 1]
Push 3:    [3, 2, 1]
Pop:       [2, 1]  (removed 3 - last in)
```

**Queue (FIFO)**:
```
Enqueue 1:  [1]
Enqueue 2:  [1, 2]
Enqueue 3:  [1, 2, 3]
Dequeue:    [2, 3]  (removed 1 - first in)
```

***

## Part 15: Complete Working Examples

### Example 1: Browser History (Stack)

```python
class BrowserHistory:
    def __init__(self):
        self.history = []
        self.current = "Homepage"
    
    def visit(self, url):
        self.history.append(self.current)
        self.current = url
        print(f"Visited: {url}")
    
    def back(self):
        if self.history:
            previous = self.history.pop()
            print(f"Going back from {self.current} to {previous}")
            self.current = previous
        else:
            print("No previous page")
    
    def show_current(self):
        print(f"Current page: {self.current}")

# Use it
browser = BrowserHistory()
browser.visit("google.com")
browser.visit("github.com")
browser.visit("stackoverflow.com")
browser.show_current()  # stackoverflow.com
browser.back()          # Back to github.com
browser.back()          # Back to google.com
browser.show_current()  # google.com
```

### Example 2: Task Scheduler (Queue)

```python
class TaskScheduler:
    def __init__(self):
        self.tasks = []
    
    def add_task(self, task):
        self.tasks.append(task)
        print(f"Task added: {task}")
    
    def execute_next(self):
        if self.tasks:
            task = self.tasks.pop(0)
            print(f"Executing: {task}")
        else:
            print("No tasks to execute")
    
    def show_tasks(self):
        if self.tasks:
            print(f"Pending tasks: {', '.join(self.tasks)}")
        else:
            print("No pending tasks")

# Use it
scheduler = TaskScheduler()
scheduler.add_task("Send email")
scheduler.add_task("Update database")
scheduler.add_task("Generate report")
scheduler.show_tasks()      # Pending: Send email, Update database, Generate report
scheduler.execute_next()    # Executing: Send email
scheduler.execute_next()    # Executing: Update database
scheduler.show_tasks()      # Pending: Generate report
```

***

## Part 16: Key Points to Remember

### Stack (LIFO)
1. **Last In, First Out** - Like a stack of plates
2. **Operations**: Push (add), Pop (remove), Peek (view)
3. **Time**: O(1) for all main operations
4. **Uses**: Undo, function calls, backtracking, expression evaluation
5. **Think**: "Stack of books on a desk"

### Queue (FIFO)
1. **First In, First Out** - Like a line at a store
2. **Operations**: Enqueue (add), Dequeue (remove), Peek (view)
3. **Time**: O(1) for enqueue, O(n) for dequeue (with list), O(1) with deque
4. **Uses**: Task scheduling, print jobs, breadth-first search
5. **Think**: "People waiting in line"

***

## Part 17: Practice Exercises

### Exercise 1: Stack Practice
Create a stack and:
1. Push the numbers 1, 2, 3, 4, 5
2. Pop two elements
3. Push 6 and 7
4. Display the final stack

### Exercise 2: Queue Practice
Create a queue and:
1. Enqueue "A", "B", "C", "D"
2. Dequeue one element
3. Enqueue "E"
4. Display the final queue

### Exercise 3: Challenge
Write a function that uses a stack to check if a string is a palindrome (reads the same forwards and backwards).

***


--------


# TREE AND GRAPH - SUPER SIMPLE STUDY NOTES

## PART A: TREE DATA STRUCTURE

## Part 1: What is a Tree?

A **tree** is a hierarchical data structure that looks like an upside-down tree. It consists of **nodes** connected by **edges**, where each node can have multiple children, but only one parent.

**Key Rule**: Trees are hierarchical - data flows from top to bottom, like a family tree or organizational chart.

### Real-World Analogies

1. **Family Tree**: Grandparents at top, parents below, children at bottom
2. **File System**: Folders containing subfolders and files
3. **Company Organization**: CEO at top, managers below, employees at bottom
4. **HTML DOM**: HTML structure in web pages

***

## Part 2: Tree Terminology (Essential Vocabulary)

```
         [A]  ← Root (topmost node, no parent)
        /   \
      [B]   [C]  ← Children of A
      / \     \
    [D] [E]   [F]  ← Leaf nodes (no children)
```

**Root**: The topmost node with no parent (A)

**Parent**: A node that has children (A is parent of B and C)

**Child**: A node connected below another node (B and C are children of A)

**Siblings**: Nodes with the same parent (B and C are siblings)

**Leaf (External Node)**: A node with no children (D, E, F)

**Internal Node**: A node with at least one child (A, B, C)

**Edge**: Connection between two nodes (lines connecting nodes)

**Path**: Sequence of nodes connected by edges (A → B → D)

**Height of Tree**: Longest path from root to any leaf (2 in the example above)

**Depth of Node**: Number of edges from root to that node (B has depth 1)

**Level**: All nodes at same depth (B and C are at level 1)

***

## Part 3: Types of Trees

### Binary Tree
Each node has **at most 2 children** (left and right).

```
      [10]
     /    \
   [5]    [15]
   / \      \
 [3] [7]   [20]
```

### Binary Search Tree (BST)
A binary tree where:
- Left child < Parent
- Right child > Parent

```
       [50]
      /    \
   [30]    [70]
   / \     / \
 [20][40][60][80]

Rule: 20 < 30 < 50 < 60 < 70 < 80
```

### N-ary Tree
Each node can have **n children**.

```
        [A]
      / | \ \
    [B][C][D][E]
    /\  |
  [F][G][H]
```

***

## Part 4: Simple Binary Tree in Python

### Building a Basic Tree Node

```python
class TreeNode:
    def __init__(self, data):
        self.data = data        # The value stored in the node
        self.left = None        # Pointer to left child
        self.right = None       # Pointer to right child


# Create individual nodes
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.left = TreeNode(4)
root.left.right = TreeNode(5)

# Tree structure:
#       1
#      / \
#     2   3
#    / \
#   4   5
```

***

## Part 5: Tree Traversal (Visiting All Nodes)

There are three main ways to traverse a binary tree:

### 1. In-Order Traversal (Left → Root → Right)

```python
def inorder(node):
    if node:
        inorder(node.left)       # Visit left subtree
        print(node.data, end=' ') # Visit root
        inorder(node.right)      # Visit right subtree

# Example tree:
#       1
#      / \
#     2   3
#    / \
#   4   5

# Output: 4 2 5 1 3
```

### 2. Pre-Order Traversal (Root → Left → Right)

```python
def preorder(node):
    if node:
        print(node.data, end=' ') # Visit root
        preorder(node.left)       # Visit left subtree
        preorder(node.right)      # Visit right subtree

# Example tree:
#       1
#      / \
#     2   3
#    / \
#   4   5

# Output: 1 2 4 5 3
```

### 3. Post-Order Traversal (Left → Right → Root)

```python
def postorder(node):
    if node:
        postorder(node.left)      # Visit left subtree
        postorder(node.right)     # Visit right subtree
        print(node.data, end=' ')  # Visit root

# Example tree:
#       1
#      / \
#     2   3
#    / \
#   4   5

# Output: 4 5 2 3 1
```

***

## Part 6: Complete Binary Tree Implementation

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BinaryTree:
    def __init__(self):
        self.root = None
    
    # Insert nodes (for demonstration)
    def insert(self, data):
        if self.root is None:
            self.root = TreeNode(data)
        else:
            self._insert_recursive(self.root, data)
    
    def _insert_recursive(self, node, data):
        if data < node.
            if node.left is None:
                node.left = TreeNode(data)
            else:
                self._insert_recursive(node.left, data)
        else:
            if node.right is None:
                node.right = TreeNode(data)
            else:
                self._insert_recursive(node.right, data)
    
    # In-order traversal
    def inorder(self, node=None):
        if node is None:
            node = self.root
        if node:
            self.inorder(node.left)
            print(node.data, end=' ')
            self.inorder(node.right)
    
    # Pre-order traversal
    def preorder(self, node=None):
        if node is None:
            node = self.root
        if node:
            print(node.data, end=' ')
            self.preorder(node.left)
            self.preorder(node.right)
    
    # Post-order traversal
    def postorder(self, node=None):
        if node is None:
            node = self.root
        if node:
            self.postorder(node.left)
            self.postorder(node.right)
            print(node.data, end=' ')
    
    # Search for a value
    def search(self, data, node=None):
        if node is None:
            node = self.root
        
        if node is None:
            return False
        if node.data == 
            return True
        if data < node.
            return self.search(data, node.left)
        else:
            return self.search(data, node.right)
    
    # Get height of tree
    def height(self, node=None):
        if node is None:
            node = self.root
        
        if node is None:
            return -1
        
        left_height = self.height(node.left)
        right_height = self.height(node.right)
        return max(left_height, right_height) + 1


# ===== USING THE BINARY TREE =====

tree = BinaryTree()

# Insert elements
print("Inserting elements: 50, 30, 70, 20, 40, 60, 80")
tree.insert(50)
tree.insert(30)
tree.insert(70)
tree.insert(20)
tree.insert(40)
tree.insert(60)
tree.insert(80)

# Tree structure:
#        50
#       /  \
#     30    70
#     / \   / \
#   20  40 60 80

print("\nIn-order traversal:")
tree.inorder()  # Output: 20 30 40 50 60 70 80

print("\n\nPre-order traversal:")
tree.preorder()  # Output: 50 30 20 40 70 60 80

print("\n\nPost-order traversal:")
tree.postorder()  # Output: 20 40 30 60 80 70 50

print("\n\nSearching for 40:", tree.search(40))  # True
print("Searching for 100:", tree.search(100))  # False

print("\nTree height:", tree.height())  # 2
```

***

## Part 7: Real-World Tree Applications

### Application 1: File System

```python
class FileNode:
    def __init__(self, name, is_file=False):
        self.name = name
        self.is_file = is_file
        self.children = []
    
    def add_child(self, child):
        self.children.append(child)
    
    def display(self, level=0):
        indent = "  " * level
        print(f"{indent}{self.name}")
        for child in self.children:
            child.display(level + 1)

# Create file system
root = FileNode("C:")
documents = FileNode("Documents")
pictures = FileNode("Pictures")

file1 = FileNode("resume.pdf", is_file=True)
file2 = FileNode("photo.jpg", is_file=True)

root.add_child(documents)
root.add_child(pictures)
documents.add_child(file1)
pictures.add_child(file2)

root.display()
# Output:
# C:
#   Documents
#     resume.pdf
#   Pictures
#     photo.jpg
```

### Application 2: Expression Tree

```python
# Expression: (3 + 5) * 2
class ExpressionNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

# Build tree
root = ExpressionNode('*')
root.left = ExpressionNode('+')
root.right = ExpressionNode(2)
root.left.left = ExpressionNode(3)
root.left.right = ExpressionNode(5)

# Tree structure:
#       *
#      / \
#     +   2
#    / \
#   3   5

def evaluate(node):
    if node.left is None and node.right is None:
        return node.value
    
    left_val = evaluate(node.left)
    right_val = evaluate(node.right)
    
    if node.value == '+':
        return left_val + right_val
    elif node.value == '*':
        return left_val * right_val

print(evaluate(root))  # Output: 16 (because (3+5)*2 = 16)
```

***

## PART B: GRAPH DATA STRUCTURE

## Part 8: What is a Graph?

A **graph** is a collection of **nodes (vertices)** connected by **edges (links)**. Unlike trees, graphs can have cycles and any node can connect to any other node.

**Key Difference from Trees**: 
- Trees have hierarchy, one root, no cycles
- Graphs have no hierarchy, no root, can have cycles

### Real-World Analogies

1. **Social Network**: People (nodes) connected by friendships (edges)
2. **Road Map**: Cities (nodes) connected by roads (edges)
3. **Flight Routes**: Airports (nodes) connected by flights (edges)
4. **Internet**: Web pages (nodes) connected by links (edges)

***

## Part 9: Graph Terminology

```
    A --- B
    |     |
    |     |
    C --- D
```

**Vertex (Node)**: Individual points (A, B, C, D)

**Edge**: Connection between two vertices (A-B, A-C, B-D, C-D)

**Adjacent**: Two vertices connected by an edge (A and B are adjacent)

**Degree**: Number of edges connected to a vertex (A has degree 2)

**Path**: Sequence of vertices connected by edges (A → B → D)

**Cycle**: Path that starts and ends at the same vertex (A → B → D → C → A)

**Connected Graph**: Every vertex has a path to every other vertex

**Disconnected Graph**: Some vertices cannot reach others

***

## Part 10: Types of Graphs

### Undirected Graph
Edges have no direction (two-way).

```
    A --- B
    |     |
    C --- D

A-B means you can go A→B or B→A
```

### Directed Graph (Digraph)
Edges have direction (one-way).

```
    A → B
    ↓   ↓
    C → D

A→B means you can only go from A to B
```

### Weighted Graph
Edges have weights (costs, distances).

```
    A --5-- B
    |       |
    3       2
    |       |
    C --7-- D

5, 3, 2, 7 are weights (e.g., distances in km)
```

***

## Part 11: Graph Representation

### Method 1: Adjacency List (Most Common)

```python
# Undirected graph
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A', 'D'],
    'D': ['B', 'C']
}

# Visual representation:
#     A --- B
#     |     |
#     C --- D
```

### Method 2: Adjacency Matrix

```python
# 0 = no edge, 1 = edge exists
#     A  B  C  D
graph = [
    [0, 1, 1, 0],  # A
    [1, 0, 0, 1],  # B
    [1, 0, 0, 1],  # C
    [0, 1, 1, 0]   # D
]
```

***

## Part 12: Simple Graph Implementation

```python
class Graph:
    def __init__(self):
        self.graph = {}  # Adjacency list
    
    # Add a vertex
    def add_vertex(self, vertex):
        if vertex not in self.graph:
            self.graph[vertex] = []
            print(f"Added vertex: {vertex}")
    
    # Add an edge (undirected)
    def add_edge(self, vertex1, vertex2):
        if vertex1 in self.graph and vertex2 in self.graph:
            self.graph[vertex1].append(vertex2)
            self.graph[vertex2].append(vertex1)
            print(f"Added edge: {vertex1} - {vertex2}")
    
    # Display graph
    def display(self):
        print("\nGraph structure:")
        for vertex in self.graph:
            print(f"{vertex}: {self.graph[vertex]}")
    
    # Get all neighbors of a vertex
    def get_neighbors(self, vertex):
        if vertex in self.graph:
            return self.graph[vertex]
        return []
    
    # Check if edge exists
    def has_edge(self, vertex1, vertex2):
        if vertex1 in self.graph:
            return vertex2 in self.graph[vertex1]
        return False


# ===== USING THE GRAPH =====

g = Graph()

# Add vertices
g.add_vertex('A')
g.add_vertex('B')
g.add_vertex('C')
g.add_vertex('D')

# Add edges
g.add_edge('A', 'B')
g.add_edge('A', 'C')
g.add_edge('B', 'D')
g.add_edge('C', 'D')

# Display
g.display()
# Output:
# A: ['B', 'C']
# B: ['A', 'D']
# C: ['A', 'D']
# D: ['B', 'C']

# Get neighbors
print(f"\nNeighbors of A: {g.get_neighbors('A')}")  # ['B', 'C']

# Check edge
print(f"Edge A-B exists? {g.has_edge('A', 'B')}")  # True
print(f"Edge A-D exists? {g.has_edge('A', 'D')}")  # False
```

***

## Part 13: Graph Traversal Algorithms

### Breadth-First Search (BFS)
Explore all neighbors first, then their neighbors (level by level).

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    result = []
    
    while queue:
        vertex = queue.popleft()
        
        if vertex not in visited:
            visited.add(vertex)
            result.append(vertex)
            
            # Add all unvisited neighbors to queue
            for neighbor in graph[vertex]:
                if neighbor not in visited:
                    queue.append(neighbor)
    
    return result

# Example usage
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}

print("BFS from A:", bfs(graph, 'A'))
# Output: ['A', 'B', 'C', 'D', 'E', 'F']
# (visits level by level)
```

### Depth-First Search (DFS)
Explore as far as possible, then backtrack.

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    
    visited.add(start)
    result = [start]
    
    for neighbor in graph[start]:
        if neighbor not in visited:
            result.extend(dfs(graph, neighbor, visited))
    
    return result

# Example usage
print("DFS from A:", dfs(graph, 'A'))
# Output: ['A', 'B', 'D', 'E', 'F', 'C']
# (goes deep first)
```

***

## Part 14: Real-World Graph Applications

### Application 1: Social Network

```python
class SocialNetwork:
    def __init__(self):
        self.network = {}
    
    def add_person(self, name):
        if name not in self.network:
            self.network[name] = []
    
    def add_friendship(self, person1, person2):
        if person1 in self.network and person2 in self.network:
            self.network[person1].append(person2)
            self.network[person2].append(person1)
    
    def get_friends(self, person):
        return self.network.get(person, [])
    
    def mutual_friends(self, person1, person2):
        friends1 = set(self.network.get(person1, []))
        friends2 = set(self.network.get(person2, []))
        return list(friends1.intersection(friends2))

# Use it
social = SocialNetwork()
social.add_person("Alice")
social.add_person("Bob")
social.add_person("Charlie")
social.add_person("Diana")

social.add_friendship("Alice", "Bob")
social.add_friendship("Alice", "Charlie")
social.add_friendship("Bob", "Charlie")
social.add_friendship("Charlie", "Diana")

print("Alice's friends:", social.get_friends("Alice"))  # ['Bob', 'Charlie']
print("Mutual friends of Alice and Diana:", 
      social.mutual_friends("Alice", "Diana"))  # ['Charlie']
```

### Application 2: Route Finder

```python
def find_path(graph, start, end, path=[]):
    path = path + [start]
    
    if start == end:
        return path
    
    if start not in graph:
        return None
    
    for node in graph[start]:
        if node not in path:
            new_path = find_path(graph, node, end, path)
            if new_path:
                return new_path
    
    return None

# City map
city_map = {
    'Home': ['Park', 'Mall'],
    'Park': ['Home', 'School'],
    'Mall': ['Home', 'Office'],
    'School': ['Park', 'Office'],
    'Office': ['Mall', 'School']
}

path = find_path(city_map, 'Home', 'Office')
print("Path from Home to Office:", ' → '.join(path))
# Output: Home → Mall → Office
```

***

## Part 15: Tree vs Graph Comparison

| Feature | Tree | Graph |
|---------|------|-------|
| **Structure** | Hierarchical | Network |
| **Root** | Has one root | No specific root |
| **Cycles** | No cycles allowed | Can have cycles |
| **Edges** | N nodes = N-1 edges | Any number of edges |
| **Parent-Child** | Each node has 1 parent | No parent-child concept |
| **Connection** | Always connected | Can be disconnected |
| **Example** | File system, family tree | Social network, maps |

### Visual Comparison

**Tree**:
```
     Root
      |
    /   \
   A     B
  / \     \
 C   D     E

- One root
- Hierarchical
- No cycles
```

**Graph**:
```
   A --- B
   |  X  |
   | / \ |
   C --- D

- No root
- Any node can connect to any
- Can have cycles (A→B→D→C→A)
```

***

## Part 16: Key Points to Remember

### Trees
1. **Hierarchical structure** - Parent-child relationships
2. **One root** - Starting point at top
3. **No cycles** - Can't loop back
4. **Connected** - All nodes reachable from root
5. **Uses**: File systems, DOM, databases, decision trees
6. **Traversal**: In-order, pre-order, post-order

### Graphs
1. **Network structure** - Nodes can connect to any node
2. **No root** - No starting point
3. **Can have cycles** - Loops allowed
4. **Can be disconnected** - Some nodes unreachable
5. **Uses**: Social networks, maps, routing, recommendations
6. **Traversal**: BFS (breadth-first), DFS (depth-first)

***

## Part 17: Time Complexity Summary

| Operation | Tree (BST) | Graph |
|-----------|-----------|-------|
| **Search** | O(log n) average | O(V + E) |
| **Insert** | O(log n) average | O(1) add vertex, O(1) add edge |
| **Delete** | O(log n) average | O(V) for vertex, O(E) for edge |
| **Traversal** | O(n) | O(V + E) |

V = number of vertices, E = number of edges

***

## Part 18: Practice Exercises

### Tree Exercise
1. Create a binary tree with values: 50, 30, 70, 20, 40, 60, 80
2. Perform in-order, pre-order, and post-order traversals
3. Search for value 40
4. Find the height of the tree

### Graph Exercise
1. Create a graph representing 5 friends and their friendships
2. Implement BFS to find all friends reachable from a starting person
3. Find if there's a path between two people
4. Count mutual friends between two people

***


