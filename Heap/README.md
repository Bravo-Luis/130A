# Priority Queue

## Operations

### Basic
- insert(element)
- element = deleteMin() or deleteMax()

### Sometimes
- increaseKey(element, amount)
- decreaseKey(element, amount)
- remove(element)
- newQueue = union(oldQueue1, oldQueue2)

## Implementations

### Unordered linked list
- insert O(1)
- deleteMin/DeleteMax O(n)

### Ordered linked list
- insert O(n)
- deleteMin/DeleteMax O(1)

### Balanced binary search tree
- insert, deleteMin/deleteMax O(logn)
- increaseKey, decreaseKey, remove O(logn)
- union O(n)
- height will always be log n

### Heap Binary Heap
- same performance as bst implementation
- much simpler to implement

## Heap Implementation

### Tree Structure: Complete Binary Tree
- One element per node
- Tree filled level by level
    - Only vacancies are at the bottom, to the right
- A binary heap with n nodes has height O(log n)

<img width="625" alt="Screenshot 2023-03-16 at 4 00 36 AM" src="https://user-images.githubusercontent.com/91937163/225597398-816203b9-f044-4994-a533-9e424a479b27.png">

### Heap Property
- key(parent) < key(child) at all nodes (Min Heap)
    - min key at the root
- key(parent) > key(child) at all nodes (Max Heap)
    - max key at the root

### Maintaining Heap Property after Insertion or DeleteMin/DeleteMax
- percolateUp
    - used for **insert** and decreaseKey
- percolateDown
    - used for **delete** and increaseKey

``` python
# MinHeap Percolate Pseudocode
# PercolateUp Pseudocode 
percolateUp(e):
    while key(e) < key(parent of e):
        swap e with its parent

# PercolateDown Pseudocode 
percolateDown(e):
    while key(e) > key(some child of e):
        swap e with its smallest child
```

### Decrease or Increase key
- Must know where element is; there's no find function

``` python
#DecreaseKey pseudocode
DecreaseKey(element, amount):
    key(element) = key(element) - amount
    percolateUp(element)

#IncreaseKey pseudocode
IncreaseKey(element, amount):
    key(element) = key(element) + amount
    percolateDown(element)
```

### Inserting
- insert(element)
- add element as a new leaf,(in binary heap this just means the end of the array)
- percolateUp from the newly added element
- O(log n)

### Deleting
- return element currently at the root
- swap it with some leaf (in binary heap should be last leaf in array)
- percolateDown from root
- O(log n)

## Array Representation

<img width="893" alt="Screenshot 2023-03-15 at 8 56 49 PM" src="https://user-images.githubusercontent.com/91937163/225597505-d2a0b218-3789-444c-9de8-834e5ca04833.png">

- for parent i
    - left child = 2i
    - right child = 2i + 1

### Sorting with HEAPIFY
- start with unordered array
- start sorting at the middle index (which is the last non-leaf node)
- go through each element with if statements after every change percolate down
- O(n) sorting

### BUILD HEAP
- rather than sorting a heap after building it O(n log n)
- build the whole heap at once
- O(n)

``` C++
template<class comparable>
BinaryHeap<comparable>::buildHeap()
    for (int i = currentSize / 2; 1 > 0; i--)
        percolateDown(i)
```

TODO: ADD Mergeable heaps / leftist tree
