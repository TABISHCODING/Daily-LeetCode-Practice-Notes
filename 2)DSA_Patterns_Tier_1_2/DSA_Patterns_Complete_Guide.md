# Ultimate DSA Patterns Guide - Complete Edition
## Master All Coding Patterns from Basic to Advanced

---

## 📚 Table of Contents

### TIER 1: Foundation Patterns (Weeks 1-2)
1. Two Pointers
2. Sliding Window
3. Fast & Slow Pointers
4. Prefix Sum

### TIER 2: Search & Sort Patterns (Weeks 3-4)
5. Binary Search
6. Hash Map & Hash Set
7. Sorting Techniques

### TIER 3: Stack & Queue Patterns (Week 5)
8. Stack Operations
9. Monotonic Stack
10. Queue & Deque

### TIER 4: Linked List Patterns (Week 6)
11. Linked List Operations
12. In-place Reversal of LinkedList

### TIER 5: Tree Patterns (Weeks 7-8)
13. Tree Traversals (DFS)
14. Tree BFS (Level Order)
15. Binary Search Tree

### TIER 6: Heap Patterns (Week 9)
16. Heap/Priority Queue
17. Top K Elements

### TIER 7: Graph Patterns (Weeks 10-11)
18. Graph DFS
19. Graph BFS
20. Topological Sort
21. Union-Find (Disjoint Set)

### TIER 8: Interval Patterns (Week 12)
22. Merge Intervals
23. Interval Scheduling

### TIER 9: Matrix Patterns (Week 13)
24. Matrix Traversal
25. 2D Dynamic Programming

### TIER 10: Advanced Patterns (Weeks 14-18)
26. Backtracking
27. Dynamic Programming
28. Greedy Algorithms
29. Bit Manipulation
30. Trie (Prefix Tree)

---

# TIER 1: Foundation Patterns (Weeks 1-2)

## 1. Two Pointers Pattern

### 📖 What is it?
Two Pointers technique uses two indices to traverse through data structures, typically from opposite ends or at different speeds. This eliminates the need for nested loops in many scenarios.

### 🎯 When to Use?
- **Sorted Arrays**: Working with sorted/partially sorted arrays
- **Finding Pairs**: Need to find pairs that satisfy a condition (sum, difference)
- **Palindrome Checking**: Comparing elements from both ends
- **Removing Duplicates**: In-place array modifications
- **Partitioning**: Separating elements based on criteria

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Pair of elements"
- "Sorted array"
- "Compare from both ends"
- "Remove duplicates in-place"
- "Partition array"
- "Find triplets/quadruplets"
- "Palindrome"

**Problem Characteristics:**
- Array or string is sorted (or can be sorted)
- Need to find pairs/triplets
- Need to compare elements from different positions
- In-place operations required

### 💡 Pattern Variations

#### Variation 1: Opposite Direction (Start & End)
```python
def two_pointer_opposite(arr, target):
    """
    Pointers move from opposite ends towards center
    Used for: Two Sum in sorted array, Container with water
    """
    left = 0
    right = len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1  # Need larger sum
        else:
            right -= 1  # Need smaller sum
    
    return [-1, -1]

# Time: O(n), Space: O(1)
```

#### Variation 2: Same Direction (Slow & Fast)
```python
def remove_duplicates(nums):
    """
    Both pointers move in same direction at different speeds
    Used for: Remove duplicates, move zeros
    """
    if not nums:
        return 0
    
    slow = 0  # Position for next unique element
    
    for fast in range(1, len(nums)):
        if nums[fast] != nums[slow]:
            slow += 1
            nums[slow] = nums[fast]
    
    return slow + 1

# Time: O(n), Space: O(1)
```

#### Variation 3: Multiple Pointers (3+ pointers)
```python
def three_sum(nums):
    """
    Uses one fixed pointer + two moving pointers
    Used for: 3Sum, 4Sum problems
    """
    nums.sort()
    result = []
    
    for i in range(len(nums) - 2):
        # Skip duplicates for first number
        if i > 0 and nums[i] == nums[i-1]:
            continue
        
        left = i + 1
        right = len(nums) - 1
        target = -nums[i]
        
        while left < right:
            current_sum = nums[left] + nums[right]
            
            if current_sum == target:
                result.append([nums[i], nums[left], nums[right]])
                
                # Skip duplicates
                while left < right and nums[left] == nums[left+1]:
                    left += 1
                while left < right and nums[right] == nums[right-1]:
                    right -= 1
                
                left += 1
                right -= 1
            elif current_sum < target:
                left += 1
            else:
                right -= 1
    
    return result

# Time: O(n²), Space: O(1) excluding output
```

### 📝 Problem Categories & Difficulty Progression

#### Beginner (Easy)
1. **Two Sum II - Input Array Is Sorted** (LC #167)
   - Classic opposite direction two pointers
   - Find two numbers that sum to target

2. **Valid Palindrome** (LC #125)
   - Check if string is palindrome
   - Compare from both ends

3. **Remove Duplicates from Sorted Array** (LC #26)
   - Same direction, different speeds
   - In-place modification

4. **Move Zeroes** (LC #283)
   - Move all zeros to end
   - Maintain relative order

5. **Merge Sorted Array** (LC #88)
   - Merge two sorted arrays
   - Three pointers technique

#### Intermediate (Medium)
6. **3Sum** (LC #15)
   - Find all unique triplets that sum to zero
   - Fixed pointer + two moving pointers

7. **Container With Most Water** (LC #11)
   - Find max area between vertical lines
   - Greedy approach with two pointers

8. **3Sum Closest** (LC #16)
   - Find triplet closest to target sum

9. **Sort Colors** (LC #75)
   - Dutch National Flag problem
   - Three-way partitioning

10. **Remove Duplicates from Sorted Array II** (LC #80)
    - Allow at most 2 duplicates

#### Advanced (Hard)
11. **Trapping Rain Water** (LC #42)
    - Calculate trapped rainwater
    - Two pointer or DP approach

12. **4Sum** (LC #18)
    - Find all unique quadruplets
    - Generalization of 3Sum

---

## 2. Sliding Window Pattern

### 📖 What is it?
Sliding Window maintains a window (subarray/substring) that slides through the array/string. The window can be fixed-size or variable-size based on conditions.

### 🎯 When to Use?
- **Contiguous Subarrays/Substrings**: Finding properties of subarrays
- **Optimization Problems**: Max/min of subarrays
- **String Matching**: Pattern matching, anagrams
- **Running Calculations**: Moving averages, sums

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Contiguous subarray/substring"
- "Maximum/minimum of all subarrays"
- "Longest/shortest substring"
- "Window of size K"
- "All subarrays of size K"
- "Characters/elements that appear"

**Problem Characteristics:**
- Need to process contiguous elements
- Looking for optimal subarray/substring
- Constraints on window contents (e.g., distinct characters)

### 💡 Pattern Variations

#### Variation 1: Fixed Size Window
```python
def max_sum_subarray(arr, k):
    """
    Fixed window size K
    Used for: Maximum sum of subarray of size K
    """
    if len(arr) < k:
        return -1
    
    # Calculate sum of first window
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    # Slide the window
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum

# Time: O(n), Space: O(1)
```

#### Variation 2: Variable Size Window (Shrinkable)
```python
def longest_substring_k_distinct(s, k):
    """
    Variable window that shrinks when condition violated
    Used for: Longest substring with K distinct characters
    """
    char_count = {}
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        # Expand window
        char_count[s[right]] = char_count.get(s[right], 0) + 1
        
        # Shrink window if needed
        while len(char_count) > k:
            char_count[s[left]] -= 1
            if char_count[s[left]] == 0:
                del char_count[s[left]]
            left += 1
        
        # Update result
        max_length = max(max_length, right - left + 1)
    
    return max_length

# Time: O(n), Space: O(k)
```

#### Variation 3: Two Pointers with Condition
```python
def min_window_substring(s, t):
    """
    Find minimum window containing all characters of t
    Used for: Minimum Window Substring
    """
    from collections import Counter
    
    if not s or not t:
        return ""
    
    dict_t = Counter(t)
    required = len(dict_t)
    formed = 0
    
    window_counts = {}
    left = 0
    min_len = float('inf')
    min_left = 0
    
    for right in range(len(s)):
        # Add character to window
        char = s[right]
        window_counts[char] = window_counts.get(char, 0) + 1
        
        # Check if frequency matches
        if char in dict_t and window_counts[char] == dict_t[char]:
            formed += 1
        
        # Try to minimize window
        while left <= right and formed == required:
            # Update result
            if right - left + 1 < min_len:
                min_len = right - left + 1
                min_left = left
            
            # Remove from left
            char = s[left]
            window_counts[char] -= 1
            if char in dict_t and window_counts[char] < dict_t[char]:
                formed -= 1
            
            left += 1
    
    return "" if min_len == float('inf') else s[min_left:min_left + min_len]

# Time: O(|S| + |T|), Space: O(|S| + |T|)
```

### 📝 Problem Categories & Difficulty Progression

#### Beginner (Easy)
1. **Maximum Average Subarray I** (LC #643)
   - Fixed window size
   - Find maximum average

2. **Contains Duplicate II** (LC #219)
   - Check if duplicate exists within K distance

3. **Max Consecutive Ones III** (LC #1004)
   - Flip at most K zeros

#### Intermediate (Medium)
4. **Longest Substring Without Repeating Characters** (LC #3)
   - Variable window
   - Track unique characters

5. **Longest Repeating Character Replacement** (LC #424)
   - Can replace K characters
   - Find longest uniform substring

6. **Permutation in String** (LC #567)
   - Check if s2 contains permutation of s1
   - Fixed size window with character count

7. **Find All Anagrams in a String** (LC #438)
   - Find all anagram positions
   - Sliding window with frequency matching

8. **Minimum Size Subarray Sum** (LC #209)
   - Find minimum length subarray with sum ≥ target

9. **Fruit Into Baskets** (LC #904)
   - Pick fruit from at most 2 types of trees

10. **Subarray Product Less Than K** (LC #713)
    - Count subarrays with product < K

#### Advanced (Hard)
11. **Minimum Window Substring** (LC #76)
    - Most comprehensive sliding window problem
    - Find minimum window containing all characters

12. **Sliding Window Maximum** (LC #239)
    - Find maximum in each window of size K
    - Uses deque for optimization

13. **Substring with Concatenation of All Words** (LC #30)
    - Multiple word matching

---

## 3. Fast & Slow Pointers Pattern

### 📖 What is it?
Fast & Slow Pointers (also called Tortoise and Hare) uses two pointers that move at different speeds. Fast pointer moves twice as fast as slow pointer.

### 🎯 When to Use?
- **Cycle Detection**: Finding cycles in linked lists
- **Middle Element**: Finding middle of linked list
- **Palindrome Check**: For linked lists
- **Loop Detection**: In sequences or linked structures

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Cycle in linked list"
- "Middle element"
- "Detect loop"
- "Happy number"
- "Circular array"
- "Find duplicate"

**Problem Characteristics:**
- Linked list or sequence with potential cycle
- Need to find middle element
- Constant space requirement

### 💡 Pattern Variations

#### Variation 1: Cycle Detection
```python
def has_cycle(head):
    """
    Detect if linked list has cycle
    Floyd's Cycle Detection Algorithm
    """
    if not head or not head.next:
        return False
    
    slow = head
    fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            return True
    
    return False

# Time: O(n), Space: O(1)
```

#### Variation 2: Find Cycle Start
```python
def detect_cycle(head):
    """
    Find the node where cycle begins
    """
    if not head or not head.next:
        return None
    
    # Phase 1: Detect cycle
    slow = fast = head
    has_cycle = False
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            has_cycle = True
            break
    
    if not has_cycle:
        return None
    
    # Phase 2: Find cycle start
    slow = head
    while slow != fast:
        slow = slow.next
        fast = fast.next
    
    return slow

# Time: O(n), Space: O(1)
```

#### Variation 3: Find Middle Element
```python
def find_middle(head):
    """
    Find middle node of linked list
    When fast reaches end, slow is at middle
    """
    if not head:
        return None
    
    slow = fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    return slow

# Time: O(n), Space: O(1)
```

#### Variation 4: Palindrome Check
```python
def is_palindrome(head):
    """
    Check if linked list is palindrome
    1. Find middle
    2. Reverse second half
    3. Compare both halves
    """
    if not head or not head.next:
        return True
    
    # Find middle
    slow = fast = head
    while fast.next and fast.next.next:
        slow = slow.next
        fast = fast.next.next
    
    # Reverse second half
    second_half = reverse_list(slow.next)
    
    # Compare
    first_half = head
    while second_half:
        if first_half.val != second_half.val:
            return False
        first_half = first_half.next
        second_half = second_half.next
    
    return True

def reverse_list(head):
    prev = None
    current = head
    while current:
        next_temp = current.next
        current.next = prev
        prev = current
        current = next_temp
    return prev

# Time: O(n), Space: O(1)
```

### 📝 Problem Categories & Difficulty Progression

#### Beginner (Easy)
1. **Linked List Cycle** (LC #141)
   - Classic cycle detection

2. **Middle of the Linked List** (LC #876)
   - Find middle node

3. **Happy Number** (LC #202)
   - Detect cycle in number sequence

4. **Remove Duplicates from Sorted List** (LC #83)
   - Use slow pointer for unique elements

#### Intermediate (Medium)
5. **Linked List Cycle II** (LC #142)
   - Find where cycle begins

6. **Find the Duplicate Number** (LC #287)
   - Array as linked list
   - Finding cycle in array

7. **Palindrome Linked List** (LC #234)
   - Find middle + reverse + compare

8. **Remove Nth Node From End of List** (LC #19)
   - Fast pointer moves N steps ahead

9. **Reorder List** (LC #143)
   - Find middle + reverse + merge

10. **Circular Array Loop** (LC #457)
    - Detect cycle with direction constraint

---

## 4. Prefix Sum Pattern

### 📖 What is it?
Prefix Sum preprocesses an array to create cumulative sums, enabling O(1) range sum queries. Each element at index i contains sum of all elements from start to i.

### 🎯 When to Use?
- **Range Queries**: Multiple range sum queries
- **Subarray Sum**: Finding subarrays with specific sum
- **Cumulative Operations**: Running totals, averages
- **2D Arrays**: Matrix range queries

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Range sum query"
- "Subarray sum equals K"
- "Continuous subarray"
- "Sum of elements between indices"
- "Maximum/minimum subarray sum"
- "Count of subarrays"

**Problem Characteristics:**
- Multiple queries on same array
- Finding subarrays with specific sum
- Need for cumulative data

### 💡 Pattern Variations

#### Variation 1: Basic Prefix Sum
```python
class PrefixSum:
    """
    Precompute prefix sums for O(1) range queries
    """
    def __init__(self, nums):
        self.prefix = [0]
        for num in nums:
            self.prefix.append(self.prefix[-1] + num)
    
    def range_sum(self, left, right):
        """
        Sum of elements from index left to right (inclusive)
        """
        return self.prefix[right + 1] - self.prefix[left]

# Time: O(n) preprocessing, O(1) per query
# Space: O(n)
```

#### Variation 2: Prefix Sum + HashMap
```python
def subarray_sum_equals_k(nums, k):
    """
    Count subarrays with sum = k
    Uses prefix sum + hash map
    """
    count = 0
    prefix_sum = 0
    sum_count = {0: 1}  # Base case
    
    for num in nums:
        prefix_sum += num
        
        # Check if (prefix_sum - k) exists
        if prefix_sum - k in sum_count:
            count += sum_count[prefix_sum - k]
        
        # Add current prefix sum to map
        sum_count[prefix_sum] = sum_count.get(prefix_sum, 0) + 1
    
    return count

# Time: O(n), Space: O(n)
```

#### Variation 3: 2D Prefix Sum
```python
class NumMatrix:
    """
    2D prefix sum for matrix range queries
    """
    def __init__(self, matrix):
        if not matrix or not matrix[0]:
            return
        
        rows, cols = len(matrix), len(matrix[0])
        self.prefix = [[0] * (cols + 1) for _ in range(rows + 1)]
        
        for i in range(1, rows + 1):
            for j in range(1, cols + 1):
                self.prefix[i][j] = (
                    matrix[i-1][j-1] +
                    self.prefix[i-1][j] +
                    self.prefix[i][j-1] -
                    self.prefix[i-1][j-1]
                )
    
    def sum_region(self, row1, col1, row2, col2):
        """
        Sum of rectangle from (row1,col1) to (row2,col2)
        """
        return (
            self.prefix[row2+1][col2+1] -
            self.prefix[row1][col2+1] -
            self.prefix[row2+1][col1] +
            self.prefix[row1][col1]
        )

# Time: O(m*n) preprocessing, O(1) per query
# Space: O(m*n)
```

### 📝 Problem Categories & Difficulty Progression

#### Beginner (Easy)
1. **Range Sum Query - Immutable** (LC #303)
   - Basic 1D prefix sum

2. **Running Sum of 1d Array** (LC #1480)
   - Generate prefix sum array

3. **Find Pivot Index** (LC #724)
   - Left sum equals right sum

#### Intermediate (Medium)
4. **Subarray Sum Equals K** (LC #560)
   - Prefix sum + hash map
   - Count subarrays

5. **Contiguous Array** (LC #525)
   - Equal number of 0s and 1s
   - Transform to sum problem

6. **Product of Array Except Self** (LC #238)
   - Prefix products from both directions

7. **Continuous Subarray Sum** (LC #523)
   - Sum divisible by K
   - Modulo arithmetic

8. **Subarray Sums Divisible by K** (LC #974)
   - Count subarrays divisible by K

9. **Maximum Subarray** (LC #53)
   - Kadane's algorithm (related concept)

10. **Range Sum Query 2D - Immutable** (LC #304)
    - 2D prefix sum

---

# TIER 2: Search & Sort Patterns (Weeks 3-4)

## 5. Binary Search Pattern

### 📖 What is it?
Binary Search is a divide-and-conquer algorithm that efficiently searches sorted data by repeatedly halving the search space. Works on monotonic (sorted/rotated sorted) data.

### 🎯 When to Use?
- **Sorted Data**: Array/list is sorted
- **Search Space Reduction**: Can eliminate half of possibilities
- **Finding Boundaries**: First/last occurrence
- **Optimization**: Minimizing/maximizing with constraint
- **Search Answer Space**: When answer has monotonic property

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Sorted array"
- "Find element in O(log n)"
- "Rotated sorted array"
- "First/last occurrence"
- "Smallest/largest value that satisfies"
- "Minimum/maximum capacity"
- "Search in range"

**Problem Characteristics:**
- Data is sorted or partially sorted
- Need O(log n) time complexity
- Can make decision based on mid element
- Search space can be divided

### 💡 Pattern Variations

#### Variation 1: Classic Binary Search
```python
def binary_search(arr, target):
    """
    Find target in sorted array
    Returns index if found, -1 otherwise
    """
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = left + (right - left) // 2  # Avoid overflow
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1  # Search right half
        else:
            right = mid - 1  # Search left half
    
    return -1

# Time: O(log n), Space: O(1)
```

#### Variation 2: Find First/Last Occurrence
```python
def find_first_occurrence(arr, target):
    """
    Find first (leftmost) occurrence of target
    """
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if arr[mid] == target:
            result = mid
            right = mid - 1  # Continue searching left
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

def find_last_occurrence(arr, target):
    """
    Find last (rightmost) occurrence of target
    """
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if arr[mid] == target:
            result = mid
            left = mid + 1  # Continue searching right
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

# Time: O(log n), Space: O(1)
```

#### Variation 3: Binary Search on Answer Space
```python
def min_eating_speed(piles, h):
    """
    Koko Eating Bananas - Find minimum speed
    Binary search on possible speeds
    """
    def can_finish(speed):
        """Check if can finish all piles in h hours"""
        hours = 0
        for pile in piles:
            hours += (pile + speed - 1) // speed  # Ceiling division
        return hours <= h
    
    left, right = 1, max(piles)
    result = right
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if can_finish(mid):
            result = mid
            right = mid - 1  # Try slower speed
        else:
            left = mid + 1  # Need faster speed
    
    return result

# Time: O(n * log(max(piles))), Space: O(1)
```

#### Variation 4: Rotated Sorted Array
```python
def search_rotated(nums, target):
    """
    Search in rotated sorted array
    One half is always sorted
    """
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        
        # Determine which half is sorted
        if nums[left] <= nums[mid]:  # Left half is sorted
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:  # Right half is sorted
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    
    return -1

# Time: O(log n), Space: O(1)
```

### 📝 Problem Categories & Difficulty Progression

#### Beginner (Easy)
1. **Binary Search** (LC #704)
   - Classic implementation

2. **Search Insert Position** (LC #35)
   - Find insertion index

3. **First Bad Version** (LC #278)
   - Minimize API calls

4. **Sqrt(x)** (LC #69)
   - Integer square root

5. **Valid Perfect Square** (LC #367)
   - Check if perfect square

#### Intermediate (Medium)
6. **Search in Rotated Sorted Array** (LC #33)
   - Handle rotation

7. **Find Minimum in Rotated Sorted Array** (LC #153)
   - Find rotation point

8. **Find Peak Element** (LC #162)
   - Local maximum

9. **Search a 2D Matrix** (LC #74)
   - Treat as 1D array

10. **Search a 2D Matrix II** (LC #240)
    - Row and column sorted

11. **Koko Eating Bananas** (LC #875)
    - Binary search on answer

12. **Find First and Last Position** (LC #34)
    - Two binary searches

13. **Capacity To Ship Packages Within D Days** (LC #1011)
    - Minimize maximum capacity

14. **Minimum Time to Complete Trips** (LC #2187)
    - Time optimization

#### Advanced (Hard)
15. **Median of Two Sorted Arrays** (LC #4)
    - Binary search on partition

16. **Find in Mountain Array** (LC #1095)
    - Multiple binary searches

17. **Split Array Largest Sum** (LC #410)
    - Minimize maximum sum

---

## 6. Hash Map & Hash Set Pattern

### 📖 What is it?
Hash Map (Dictionary) and Hash Set provide O(1) average time for insert, delete, and lookup operations. Store key-value pairs (map) or unique elements (set).

### 🎯 When to Use?
- **Fast Lookup**: Need O(1) access time
- **Frequency Counting**: Count occurrences
- **Caching**: Store computed results
- **Uniqueness**: Remove duplicates
- **Complement Finding**: Two Sum type problems

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Count frequency"
- "Find duplicate"
- "Check if exists"
- "Anagram"
- "Group by"
- "Cache/memoize"
- "O(1) lookup"

**Problem Characteristics:**
- Need fast lookups
- Counting or frequency tracking
- Detecting duplicates
- Grouping related items

### 💡 Pattern Variations

#### Variation 1: Basic Frequency Counter
```python
def find_mode(nums):
    """
    Find most frequent element(s)
    """
    from collections import Counter
    
    # Method 1: Using Counter
    freq = Counter(nums)
    max_freq = max(freq.values())
    return [k for k, v in freq.items() if v == max_freq]

    # Method 2: Manual counting
    freq = {}
    for num in nums:
        freq[num] = freq.get(num, 0) + 1
    
    max_freq = max(freq.values())
    return [k for k, v in freq.items() if v == max_freq]

# Time: O(n), Space: O(n)
```

#### Variation 2: Complement Pattern (Two Sum)
```python
def two_sum(nums, target):
    """
    Find two numbers that sum to target
    Store complement in hash map
    """
    num_to_index = {}
    
    for i, num in enumerate(nums):
        complement = target - num
        
        if complement in num_to_index:
            return [num_to_index[complement], i]
        
        num_to_index[num] = i
    
    return []

# Time: O(n), Space: O(n)
```

#### Variation 3: Grouping Pattern
```python
def group_anagrams(strs):
    """
    Group strings that are anagrams
    """
    from collections import defaultdict
    
    groups = defaultdict(list)
    
    for s in strs:
        # Sort characters as key
        key = ''.join(sorted(s))
        groups[key].append(s)
    
    return list(groups.values())

# Alternative: Use character count as key
def group_anagrams_v2(strs):
    groups = defaultdict(list)
    
    for s in strs:
        count = [0] * 26
        for c in s:
            count[ord(c) - ord('a')] += 1
        groups[tuple(count)].append(s)
    
    return list(groups.values())

# Time: O(n * k log k), Space: O(n * k)
# where n = number of strings, k = max string length
```

#### Variation 4: LRU Cache Pattern
```python
class LRUCache:
    """
    Least Recently Used Cache
    Combines HashMap + Doubly Linked List
    """
    class Node:
        def __init__(self, key=0, val=0):
            self.key = key
            self.val = val
            self.prev = None
            self.next = None
    
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = {}
        # Dummy head and tail
        self.head = self.Node()
        self.tail = self.Node()
        self.head.next = self.tail
        self.tail.prev = self.head
    
    def get(self, key):
        if key not in self.cache:
            return -1
        
        node = self.cache[key]
        self._move_to_front(node)
        return node.val
    
    def put(self, key, value):
        if key in self.cache:
            node = self.cache[key]
            node.val = value
            self._move_to_front(node)
        else:
            if len(self.cache) >= self.capacity:
                # Remove least recently used
                lru = self.tail.prev
                self._remove(lru)
                del self.cache[lru.key]
            
            # Add new node
            node = self.Node(key, value)
            self.cache[key] = node
            self._add_to_front(node)
    
    def _remove(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev
    
    def _add_to_front(self, node):
        node.next = self.head.next
        node.prev = self.head
        self.head.next.prev = node
        self.head.next = node
    
    def _move_to_front(self, node):
        self._remove(node)
        self._add_to_front(node)

# Time: O(1) for both get and put
# Space: O(capacity)
```

### 📝 Problem Categories & Difficulty Progression

#### Beginner (Easy)
1. **Two Sum** (LC #1)
   - Classic hash map problem

2. **Contains Duplicate** (LC #217)
   - Check duplicates using set

3. **Valid Anagram** (LC #242)
   - Frequency comparison

4. **Isomorphic Strings** (LC #205)
   - Character mapping

5. **Word Pattern** (LC #290)
   - Pattern matching

6. **Happy Number** (LC #202)
   - Detect cycle with set

#### Intermediate (Medium)
7. **Group Anagrams** (LC #49)
   - Grouping with sorted key

8. **Top K Frequent Elements** (LC #347)
   - Frequency + sorting/heap

9. **Longest Consecutive Sequence** (LC #128)
   - Set for O(1) lookup

10. **3Sum** (LC #15)
    - Two pointers + set for dedup

11. **4Sum II** (LC #454)
    - Split into two groups

12. **Subarray Sum Equals K** (LC #560)
    - Prefix sum + hash map

13. **Continuous Subarray Sum** (LC #523)
    - Modulo + hash map

14. **Find All Anagrams in a String** (LC #438)
    - Sliding window + frequency

15. **Longest Substring Without Repeating Characters** (LC #3)
    - Sliding window + set

#### Advanced (Medium-Hard)
16. **LRU Cache** (LC #146)
    - Hash map + doubly linked list

17. **Insert Delete GetRandom O(1)** (LC #380)
    - Hash map + array

18. **Design Twitter** (LC #355)
    - Multiple hash maps + heap

---

## 7. Sorting Techniques Pattern

### 📖 What is it?
Sorting patterns include various algorithms and techniques to order elements. Understanding when and how to use different sorting approaches.

### 🎯 When to Use?
- **Ordering Required**: Need sorted data
- **Greedy Algorithms**: Often require sorted input
- **Binary Search**: Needs sorted array
- **Optimization**: Sorted data simplifies many problems

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Sort the array"
- "In ascending/descending order"
- "Kth largest/smallest"
- "Meeting rooms"
- "Intervals"
- "Merge sorted"

### 💡 Common Sorting Patterns

#### Quick Select (Finding Kth Element)
```python
def find_kth_largest(nums, k):
    """
    Find kth largest element using QuickSelect
    Average O(n) time
    """
    def partition(left, right, pivot_idx):
        pivot = nums[pivot_idx]
        # Move pivot to end
        nums[pivot_idx], nums[right] = nums[right], nums[pivot_idx]
        
        store_idx = left
        for i in range(left, right):
            if nums[i] < pivot:
                nums[i], nums[store_idx] = nums[store_idx], nums[i]
                store_idx += 1
        
        # Move pivot to final position
        nums[store_idx], nums[right] = nums[right], nums[store_idx]
        return store_idx
    
    def select(left, right, k_smallest):
        if left == right:
            return nums[left]
        
        pivot_idx = (left + right) // 2
        pivot_idx = partition(left, right, pivot_idx)
        
        if k_smallest == pivot_idx:
            return nums[k_smallest]
        elif k_smallest < pivot_idx:
            return select(left, pivot_idx - 1, k_smallest)
        else:
            return select(pivot_idx + 1, right, k_smallest)
    
    return select(0, len(nums) - 1, len(nums) - k)

# Average Time: O(n), Worst: O(n²), Space: O(1)
```

#### Custom Comparator
```python
def largest_number(nums):
    """
    Arrange numbers to form largest number
    Custom comparator based on string concatenation
    """
    from functools import cmp_to_key
    
    def compare(x, y):
        # Compare which order gives larger number
        if x + y > y + x:
            return -1  # x should come first
        elif x + y < y + x:
            return 1   # y should come first
        else:
            return 0
    
    nums_str = [str(num) for num in nums]
    nums_str.sort(key=cmp_to_key(compare))
    
    result = ''.join(nums_str)
    return '0' if result[0] == '0' else result

# Time: O(n log n), Space: O(n)
```

### 📝 Problem Categories

#### Easy
1. **Sort Colors** (LC #75)
   - Dutch National Flag (3-way partition)

2. **Meeting Rooms** (LC #252)
   - Sort by start time

#### Medium
3. **Kth Largest Element** (LC #215)
   - QuickSelect or Heap

4. **Largest Number** (LC #179)
   - Custom comparator

5. **Sort List** (LC #148)
   - Merge sort for linked list

6. **Merge Intervals** (LC #56)
   - Sort + merge

---

Would you like me to continue with TIER 3 onwards (Stack, Queue, Linked List, Trees, Graphs, etc.)? This is getting quite long, so I'll create Part 2 of this document.
