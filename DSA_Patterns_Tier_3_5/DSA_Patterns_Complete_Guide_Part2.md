# Ultimate DSA Patterns Guide - Part 2
## Advanced Patterns (Tiers 3-10)

---

# TIER 3: Stack & Queue Patterns (Week 5)

## 8. Stack Operations Pattern

### 📖 What is it?
Stack is a Last-In-First-Out (LIFO) data structure. Elements are added and removed from the same end (top). Used for backtracking, expression evaluation, and nested structures.

### 🎯 When to Use?
- **Matching/Balancing**: Parentheses, brackets
- **Backtracking**: Undo operations
- **Expression Evaluation**: Postfix, infix
- **Nested Structures**: HTML tags, function calls
- **Recent History**: Browser back button

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Valid parentheses"
- "Balanced"
- "Nested"
- "Most recent"
- "Evaluate expression"
- "Decode string"
- "Backtrack"

### 💡 Pattern Implementations

#### Variation 1: Matching Parentheses
```python
def is_valid_parentheses(s):
    """
    Check if parentheses are balanced
    Classic stack application
    """
    stack = []
    pairs = {'(': ')', '[': ']', '{': '}'}
    
    for char in s:
        if char in pairs:
            stack.append(char)
        elif not stack or pairs[stack.pop()] != char:
            return False
    
    return len(stack) == 0

# Time: O(n), Space: O(n)
```

#### Variation 2: Min Stack (Stack with Min Operation)
```python
class MinStack:
    """
    Stack supporting push, pop, top, and getMin in O(1)
    """
    def __init__(self):
        self.stack = []
        self.min_stack = []  # Track minimums
    
    def push(self, val):
        self.stack.append(val)
        # Push to min_stack if empty or val is new minimum
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)
    
    def pop(self):
        if self.stack:
            val = self.stack.pop()
            # Remove from min_stack if it's the minimum
            if self.min_stack and val == self.min_stack[-1]:
                self.min_stack.pop()
            return val
    
    def top(self):
        return self.stack[-1] if self.stack else None
    
    def getMin(self):
        return self.min_stack[-1] if self.min_stack else None

# All operations: O(1) time, O(n) space
```

#### Variation 3: Decode String
```python
def decode_string(s):
    """
    Decode string like "3[a2[c]]" -> "accaccacc"
    Use stack to handle nested brackets
    """
    stack = []
    current_num = 0
    current_str = ""
    
    for char in s:
        if char.isdigit():
            current_num = current_num * 10 + int(char)
        elif char == '[':
            # Push current state to stack
            stack.append((current_str, current_num))
            current_str = ""
            current_num = 0
        elif char == ']':
            # Pop and construct string
            prev_str, num = stack.pop()
            current_str = prev_str + current_str * num
        else:
            current_str += char
    
    return current_str

# Time: O(maxK * n), Space: O(sum of decoded lengths)
```

### 📝 Problem Categories

#### Easy
1. **Valid Parentheses** (LC #20)
2. **Remove All Adjacent Duplicates in String** (LC #1047)
3. **Backspace String Compare** (LC #844)
4. **Baseball Game** (LC #682)

#### Medium
5. **Min Stack** (LC #155)
6. **Decode String** (LC #394)
7. **Asteroid Collision** (LC #735)
8. **Remove K Digits** (LC #402)
9. **Score of Parentheses** (LC #856)
10. **Basic Calculator** (LC #224)
11. **Basic Calculator II** (LC #227)

---

## 9. Monotonic Stack Pattern

### 📖 What is it?
Monotonic Stack maintains elements in monotonically increasing or decreasing order. Used to find next greater/smaller elements efficiently.

### 🎯 When to Use?
- **Next Greater Element**: Find next larger element
- **Next Smaller Element**: Find next smaller element
- **Range Queries**: Maximum in ranges
- **Histogram Problems**: Largest rectangle
- **Stock Span**: Days since last higher price

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Next greater"
- "Next smaller"
- "Previous greater/smaller"
- "Largest rectangle"
- "Stock span"
- "Trapping rain water"

### 💡 Pattern Implementations

#### Variation 1: Next Greater Element
```python
def next_greater_elements(nums):
    """
    For each element, find next greater element
    Returns array with next greater or -1
    """
    n = len(nums)
    result = [-1] * n
    stack = []  # Store indices
    
    for i in range(n):
        # Pop elements smaller than current
        while stack and nums[stack[-1]] < nums[i]:
            idx = stack.pop()
            result[idx] = nums[i]
        stack.append(i)
    
    return result

# Time: O(n), Space: O(n)
```

#### Variation 2: Daily Temperatures
```python
def daily_temperatures(temperatures):
    """
    How many days until warmer temperature
    """
    n = len(temperatures)
    result = [0] * n
    stack = []  # Store indices
    
    for i in range(n):
        while stack and temperatures[stack[-1]] < temperatures[i]:
            idx = stack.pop()
            result[idx] = i - idx  # Days difference
        stack.append(i)
    
    return result

# Time: O(n), Space: O(n)
```

#### Variation 3: Largest Rectangle in Histogram
```python
def largest_rectangle_area(heights):
    """
    Find largest rectangle in histogram
    Uses monotonic increasing stack
    """
    stack = []
    max_area = 0
    heights.append(0)  # Sentinel to clear stack
    
    for i, h in enumerate(heights):
        while stack and heights[stack[-1]] > h:
            height_idx = stack.pop()
            height = heights[height_idx]
            width = i if not stack else i - stack[-1] - 1
            max_area = max(max_area, height * width)
        stack.append(i)
    
    heights.pop()  # Remove sentinel
    return max_area

# Time: O(n), Space: O(n)
```

#### Variation 4: Trapping Rain Water (Stack Solution)
```python
def trap_water(height):
    """
    Calculate trapped rainwater using stack
    """
    stack = []
    water = 0
    
    for i in range(len(height)):
        while stack and height[i] > height[stack[-1]]:
            bottom = stack.pop()
            
            if not stack:
                break
            
            distance = i - stack[-1] - 1
            bounded_height = min(height[i], height[stack[-1]]) - height[bottom]
            water += distance * bounded_height
        
        stack.append(i)
    
    return water

# Time: O(n), Space: O(n)
```

### 📝 Problem Categories

#### Easy
1. **Next Greater Element I** (LC #496)

#### Medium
2. **Daily Temperatures** (LC #739)
3. **Next Greater Element II** (LC #503)
4. **Online Stock Span** (LC #901)
5. **Sum of Subarray Minimums** (LC #907)
6. **Remove Duplicate Letters** (LC #316)

#### Hard
7. **Largest Rectangle in Histogram** (LC #84)
8. **Maximal Rectangle** (LC #85)
9. **Trapping Rain Water** (LC #42)

---

## 10. Queue & Deque Pattern

### 📖 What is it?
Queue is First-In-First-Out (FIFO). Deque (Double-Ended Queue) allows insertion/deletion from both ends. Used for BFS, sliding window maximum, and level-order processing.

### 💡 Key Implementations

#### Sliding Window Maximum (Deque)
```python
def max_sliding_window(nums, k):
    """
    Maximum of each sliding window of size k
    Uses monotonic deque
    """
    from collections import deque
    
    dq = deque()  # Store indices
    result = []
    
    for i in range(len(nums)):
        # Remove indices outside window
        while dq and dq[0] < i - k + 1:
            dq.popleft()
        
        # Remove smaller elements (not useful)
        while dq and nums[dq[-1]] < nums[i]:
            dq.pop()
        
        dq.append(i)
        
        # Add to result after first window
        if i >= k - 1:
            result.append(nums[dq[0]])
    
    return result

# Time: O(n), Space: O(k)
```

### 📝 Problem Categories

#### Easy
1. **Implement Queue using Stacks** (LC #232)
2. **Implement Stack using Queues** (LC #225)

#### Medium
3. **Design Circular Queue** (LC #622)
4. **Design Circular Deque** (LC #641)

#### Hard
5. **Sliding Window Maximum** (LC #239)
6. **Shortest Subarray with Sum at Least K** (LC #862)

---

# TIER 4: Linked List Patterns (Week 6)

## 11. Linked List Operations Pattern

### 📖 What is it?
Manipulating linked list nodes through traversal, reversal, merging, and pointer manipulation. Understanding node connections is crucial.

### 🎯 When to Use?
- **Node Manipulation**: Adding, removing, reversing nodes
- **Merging**: Combining linked lists
- **Detecting Cycles**: Finding loops
- **Reordering**: Changing node order

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Linked list"
- "Reverse"
- "Merge"
- "Remove node"
- "Reorder"
- "Find middle"

### 💡 Pattern Implementations

#### Variation 1: Reverse Linked List
```python
def reverse_list(head):
    """
    Reverse entire linked list iteratively
    """
    prev = None
    current = head
    
    while current:
        next_temp = current.next
        current.next = prev
        prev = current
        current = next_temp
    
    return prev

# Recursive version
def reverse_list_recursive(head):
    if not head or not head.next:
        return head
    
    new_head = reverse_list_recursive(head.next)
    head.next.next = head
    head.next = None
    
    return new_head

# Time: O(n), Space: O(1) iterative, O(n) recursive
```

#### Variation 2: Merge Two Sorted Lists
```python
def merge_two_lists(l1, l2):
    """
    Merge two sorted linked lists
    """
    dummy = ListNode(0)
    current = dummy
    
    while l1 and l2:
        if l1.val <= l2.val:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next
    
    # Attach remaining nodes
    current.next = l1 if l1 else l2
    
    return dummy.next

# Time: O(m + n), Space: O(1)
```

#### Variation 3: Remove Nth Node From End
```python
def remove_nth_from_end(head, n):
    """
    Remove nth node from end using two pointers
    """
    dummy = ListNode(0)
    dummy.next = head
    first = second = dummy
    
    # Move first n+1 steps ahead
    for _ in range(n + 1):
        first = first.next
    
    # Move both until first reaches end
    while first:
        first = first.next
        second = second.next
    
    # Remove node
    second.next = second.next.next
    
    return dummy.next

# Time: O(n), Space: O(1)
```

#### Variation 4: Reorder List
```python
def reorder_list(head):
    """
    Reorder L0→L1→...→Ln-1→Ln to L0→Ln→L1→Ln-1→...
    1. Find middle
    2. Reverse second half
    3. Merge two halves
    """
    if not head or not head.next:
        return
    
    # Find middle
    slow = fast = head
    while fast.next and fast.next.next:
        slow = slow.next
        fast = fast.next.next
    
    # Reverse second half
    second = slow.next
    slow.next = None
    second = reverse_list(second)
    
    # Merge
    first = head
    while second:
        temp1, temp2 = first.next, second.next
        first.next = second
        second.next = temp1
        first, second = temp1, temp2

# Time: O(n), Space: O(1)
```

### 📝 Problem Categories

#### Easy
1. **Reverse Linked List** (LC #206)
2. **Merge Two Sorted Lists** (LC #21)
3. **Delete Node in a Linked List** (LC #237)
4. **Intersection of Two Linked Lists** (LC #160)

#### Medium
5. **Add Two Numbers** (LC #2)
6. **Remove Nth Node From End** (LC #19)
7. **Swap Nodes in Pairs** (LC #24)
8. **Odd Even Linked List** (LC #328)
9. **Partition List** (LC #86)
10. **Reorder List** (LC #143)
11. **Copy List with Random Pointer** (LC #138)
12. **Sort List** (LC #148)
13. **Linked List Cycle II** (LC #142)

#### Hard
14. **Reverse Nodes in k-Group** (LC #25)
15. **Merge k Sorted Lists** (LC #23)

---

## 12. In-place Reversal of LinkedList Pattern

### 📖 What is it?
Reversing parts of a linked list without using extra space. Key technique for many linked list problems.

### 💡 Pattern Implementation

```python
def reverse_between(head, left, right):
    """
    Reverse linked list from position left to right
    """
    if not head or left == right:
        return head
    
    dummy = ListNode(0)
    dummy.next = head
    prev = dummy
    
    # Move to position before left
    for _ in range(left - 1):
        prev = prev.next
    
    # Reverse the sublist
    current = prev.next
    for _ in range(right - left):
        next_node = current.next
        current.next = next_node.next
        next_node.next = prev.next
        prev.next = next_node
    
    return dummy.next

# Time: O(n), Space: O(1)
```

### 📝 Problem Categories

#### Medium
1. **Reverse Linked List II** (LC #92)
2. **Rotate List** (LC #61)
3. **Swap Nodes in Pairs** (LC #24)

#### Hard
4. **Reverse Nodes in k-Group** (LC #25)

---

# TIER 5: Tree Patterns (Weeks 7-8)

## 13. Tree Traversals (DFS) Pattern

### 📖 What is it?
Depth-First Search systematically visits all nodes by going deep before wide. Three main orders: Preorder (Root-Left-Right), Inorder (Left-Root-Right), Postorder (Left-Right-Root).

### 🎯 When to Use?
- **Tree Traversal**: Visit all nodes
- **Path Problems**: Finding paths
- **Tree Structure**: Validating BST
- **Ancestor Problems**: Finding LCA
- **Serialize/Deserialize**: Tree encoding

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Binary tree"
- "Path from root to leaf"
- "All paths"
- "Validate BST"
- "Lowest common ancestor"
- "Maximum depth"

### 💡 Pattern Implementations

#### Variation 1: Preorder Traversal
```python
def preorder_traversal(root):
    """
    Root -> Left -> Right
    """
    # Recursive
    def recursive(node):
        if not node:
            return []
        return [node.val] + recursive(node.left) + recursive(node.right)
    
    # Iterative
    def iterative(node):
        if not node:
            return []
        
        result = []
        stack = [node]
        
        while stack:
            node = stack.pop()
            result.append(node.val)
            # Push right first so left is processed first
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        
        return result
    
    return iterative(root)

# Time: O(n), Space: O(h) where h is height
```

#### Variation 2: Inorder Traversal
```python
def inorder_traversal(root):
    """
    Left -> Root -> Right
    Gives sorted order for BST
    """
    # Recursive
    def recursive(node):
        if not node:
            return []
        return recursive(node.left) + [node.val] + recursive(node.right)
    
    # Iterative
    def iterative(node):
        result = []
        stack = []
        current = node
        
        while current or stack:
            # Go to leftmost
            while current:
                stack.append(current)
                current = current.left
            
            # Process node
            current = stack.pop()
            result.append(current.val)
            
            # Go to right
            current = current.right
        
        return result
    
    return iterative(root)

# Time: O(n), Space: O(h)
```

#### Variation 3: Postorder Traversal
```python
def postorder_traversal(root):
    """
    Left -> Right -> Root
    Used for deleting trees, bottom-up calculations
    """
    # Recursive
    def recursive(node):
        if not node:
            return []
        return recursive(node.left) + recursive(node.right) + [node.val]
    
    # Iterative (using two stacks)
    def iterative(node):
        if not node:
            return []
        
        stack1 = [node]
        stack2 = []
        
        while stack1:
            node = stack1.pop()
            stack2.append(node)
            
            if node.left:
                stack1.append(node.left)
            if node.right:
                stack1.append(node.right)
        
        return [node.val for node in reversed(stack2)]
    
    return iterative(root)

# Time: O(n), Space: O(h)
```

#### Variation 4: Validate BST
```python
def is_valid_BST(root):
    """
    Validate if tree is valid binary search tree
    """
    def validate(node, min_val, max_val):
        if not node:
            return True
        
        if node.val <= min_val or node.val >= max_val:
            return False
        
        return (validate(node.left, min_val, node.val) and
                validate(node.right, node.val, max_val))
    
    return validate(root, float('-inf'), float('inf'))

# Time: O(n), Space: O(h)
```

#### Variation 5: Path Sum Problems
```python
def has_path_sum(root, targetSum):
    """
    Check if root-to-leaf path sums to target
    """
    if not root:
        return False
    
    if not root.left and not root.right:
        return root.val == targetSum
    
    return (has_path_sum(root.left, targetSum - root.val) or
            has_path_sum(root.right, targetSum - root.val))

def path_sum_all(root, targetSum):
    """
    Find all root-to-leaf paths that sum to target
    """
    def dfs(node, remaining, path, result):
        if not node:
            return
        
        path.append(node.val)
        
        if not node.left and not node.right and remaining == node.val:
            result.append(path[:])
        
        dfs(node.left, remaining - node.val, path, result)
        dfs(node.right, remaining - node.val, path, result)
        
        path.pop()  # Backtrack
    
    result = []
    dfs(root, targetSum, [], result)
    return result

# Time: O(n), Space: O(h)
```

### 📝 Problem Categories

#### Easy
1. **Binary Tree Inorder Traversal** (LC #94)
2. **Maximum Depth of Binary Tree** (LC #104)
3. **Same Tree** (LC #100)
4. **Symmetric Tree** (LC #101)
5. **Invert Binary Tree** (LC #226)
6. **Path Sum** (LC #112)
7. **Merge Two Binary Trees** (LC #617)
8. **Diameter of Binary Tree** (LC #543)

#### Medium
9. **Validate Binary Search Tree** (LC #98)
10. **Binary Tree Level Order Traversal** (LC #102)
11. **Path Sum II** (LC #113)
12. **Flatten Binary Tree to Linked List** (LC #114)
13. **Populating Next Right Pointers** (LC #116)
14. **Kth Smallest Element in BST** (LC #230)
15. **Lowest Common Ancestor of BST** (LC #235)
16. **Lowest Common Ancestor of Binary Tree** (LC #236)
17. **Path Sum III** (LC #437)
18. **Count Good Nodes in Binary Tree** (LC #1448)

#### Hard
19. **Binary Tree Maximum Path Sum** (LC #124)
20. **Serialize and Deserialize Binary Tree** (LC #297)

---

## 14. Tree BFS (Level Order) Pattern

### 📖 What is it?
Breadth-First Search visits nodes level by level using a queue. Processes all nodes at current level before moving to next level.

### 🎯 When to Use?
- **Level by Level**: Process nodes by level
- **Shortest Path**: In unweighted trees
- **Zigzag Traversal**: Alternating directions
- **Right Side View**: Rightmost nodes
- **Cousins**: Same level, different parents

### 💡 Pattern Implementation

```python
def level_order(root):
    """
    Level order traversal (BFS)
    Returns list of lists (each level)
    """
    if not root:
        return []
    
    from collections import deque
    
    result = []
    queue = deque([root])
    
    while queue:
        level_size = len(queue)
        level = []
        
        for _ in range(level_size):
            node = queue.popleft()
            level.append(node.val)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        result.append(level)
    
    return result

# Time: O(n), Space: O(w) where w is max width
```

### 📝 Problem Categories

#### Easy
1. **Binary Tree Level Order Traversal** (LC #102)
2. **Average of Levels in Binary Tree** (LC #637)
3. **Minimum Depth of Binary Tree** (LC #111)
4. **Cousins in Binary Tree** (LC #993)

#### Medium
5. **Binary Tree Level Order Traversal II** (LC #107)
6. **Binary Tree Zigzag Level Order Traversal** (LC #103)
7. **Binary Tree Right Side View** (LC #199)
8. **Populating Next Right Pointers** (LC #116, #117)
9. **All Nodes Distance K in Binary Tree** (LC #863)

---

## 15. Binary Search Tree Pattern

### 📖 What is it?
BST property: Left subtree < Node < Right subtree. Inorder traversal gives sorted order.

### 💡 Key Operations

```python
def search_BST(root, val):
    """Search in BST"""
    if not root or root.val == val:
        return root
    
    if val < root.val:
        return search_BST(root.left, val)
    else:
        return search_BST(root.right, val)

def insert_into_BST(root, val):
    """Insert into BST"""
    if not root:
        return TreeNode(val)
    
    if val < root.val:
        root.left = insert_into_BST(root.left, val)
    else:
        root.right = insert_into_BST(root.right, val)
    
    return root

def kth_smallest(root, k):
    """Kth smallest element in BST"""
    stack = []
    current = root
    count = 0
    
    while current or stack:
        while current:
            stack.append(current)
            current = current.left
        
        current = stack.pop()
        count += 1
        
        if count == k:
            return current.val
        
        current = current.right
    
    return -1

# Time: O(h + k), Space: O(h)
```

### 📝 Problem Categories

#### Easy
1. **Search in a BST** (LC #700)
2. **Minimum Distance Between BST Nodes** (LC #783)

#### Medium
3. **Validate Binary Search Tree** (LC #98)
4. **Kth Smallest Element in BST** (LC #230)
5. **Delete Node in a BST** (LC #450)
6. **Convert Sorted Array to BST** (LC #108)
7. **Inorder Successor in BST** (LC #285)

---

Let me know if you'd like me to continue with TIER 6-10 (Heaps, Graphs, Intervals, Matrix, and Advanced Patterns) in Part 3!