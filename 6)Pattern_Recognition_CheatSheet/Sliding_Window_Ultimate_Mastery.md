# 🪟 Sliding Window Mastery Guide - Master Every Window Technique

## 📘 Philosophy: Staircase Learning - Each Step is Independent

This guide teaches you **HOW TO THINK** with sliding windows through 120+ micro-questions.
**Each stair is a tiny concept → Master all stairs → Final problem becomes trivial**

**Learning Method**: Like building LEGO - master each piece first, then combine them effortlessly.

---

## 🧠 Core Sliding Window Concepts

### **The 6 Fundamental Window Operations:**

1. **EXPAND**: Add element to window (right++)
2. **SHRINK**: Remove element from window (left++)
3. **CALCULATE**: Compute window property (sum, count, max)
4. **VALIDATE**: Check if window meets condition
5. **UPDATE**: Track best/optimal window
6. **SLIDE**: Move entire window together (fixed size)

---

## 🎯 Two Main Window Types

### **Type 1: FIXED SIZE WINDOW**
- Window size is **constant** (given as K)
- Move both pointers together
- Calculate property for each position
- **Pattern**: Initialize → Slide → Update

### **Type 2: FLEXIBLE/DYNAMIC WINDOW**
- Window size **changes** based on condition
- Expand with right, shrink with left
- Find optimal window (min/max length)
- **Pattern**: Expand → Validate → Shrink → Update

---

## 📊 Pattern Breakdown with Staircase Questions

---

## 🟢 PART 1: FIXED SIZE WINDOW (CONSTANT K)

### **Core Formula:**
```python
Window size = K (constant)
Total windows = len(arr) - K + 1
Window elements: arr[i] to arr[i+K-1]
Current window size check: right - left + 1
```

---

### 🎓 STAIRCASE 1: Understanding Window Basics (10 Micro-Steps)

**🪜 Step 1.1: What is a Window?**
```
Problem: Understand what a "window" means
Array: [1, 2, 3, 4, 5], K = 3

Window 1: [1, 2, 3] (indices 0-2)
Window 2: [2, 3, 4] (indices 1-3)
Window 3: [3, 4, 5] (indices 2-4)

Each window = consecutive K elements

Task: Draw all windows for [10, 20, 30, 40], K=2
Answer: [10,20], [20,30], [30,40]
```

---

**🪜 Step 1.2: Count Total Windows**
```
Problem: How many windows exist for array of size N with window K?
Formula: N - K + 1

Example: [1,2,3,4,5], K=3
N=5, K=3 → 5-3+1 = 3 windows ✓

Practice:
- [1,2,3,4,5,6], K=4 → Answer: 3 windows
- [1,2,3], K=3 → Answer: 1 window
- [1,2,3,4], K=2 → Answer: 3 windows

Solution:
def count_windows(arr, k):
    if len(arr) < k:
        return 0
    return len(arr) - k + 1
```

---

**🪜 Step 1.3: Extract First Window**
```
Problem: Get elements of first window
Input: [5, 10, 15, 20, 25], K=3
Output: [5, 10, 15]

Practice:
- [1,2,3,4,5], K=2 → [1, 2]
- [7,8,9], K=3 → [7, 8, 9]

Solution:
def first_window(arr, k):
    return arr[0:k]  # or arr[:k]
```

---

**🪜 Step 1.4: Extract Last Window**
```
Problem: Get elements of last window
Input: [5, 10, 15, 20, 25], K=3
Output: [15, 20, 25]

Practice:
- [1,2,3,4,5], K=2 → [4, 5]
- [7,8,9], K=1 → [9]

Solution:
def last_window(arr, k):
    return arr[-k:]  # Last K elements
    # Or: arr[len(arr)-k:]
```

---

**🪜 Step 1.5: Print All Windows**
```
Problem: Display every window
Input: [1, 2, 3, 4], K=2
Output: 
  Window 1: [1, 2]
  Window 2: [2, 3]
  Window 3: [3, 4]

Solution:
def print_all_windows(arr, k):
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        print(f"Window {i+1}: {window}")

# Try: [10,20,30,40,50], K=3
```

---

**🪜 Step 1.6: Window Start and End Indices**
```
Problem: For each window, print start and end index
Input: [1, 2, 3, 4, 5], K=3
Output:
  Window 1: start=0, end=2
  Window 2: start=1, end=3
  Window 3: start=2, end=4

Pattern: start=i, end=i+K-1

Solution:
def window_indices(arr, k):
    for i in range(len(arr) - k + 1):
        start = i
        end = i + k - 1
        print(f"Window {i+1}: start={start}, end={end}")
```

---

**🪜 Step 1.7: Check if Index is in Window**
```
Problem: Is index X inside window starting at position i?
Window at i=2, K=3 contains indices [2, 3, 4]

Check: Is index 3 in window? YES
Check: Is index 5 in window? NO

Formula: i <= index < i+K

Solution:
def is_in_window(window_start, k, index):
    return window_start <= index < window_start + k

# Test: window_start=1, k=3, index=2 → True
# Test: window_start=1, k=3, index=4 → False
```

---

**🪜 Step 1.8: Get Middle Element of Window**
```
Problem: Find middle element in current window
Input: [10, 20, 30, 40, 50], K=3, window at i=1
Window: [20, 30, 40], middle = 30

Solution:
def middle_of_window(arr, window_start, k):
    mid_offset = k // 2
    return arr[window_start + mid_offset]

# Practice: [1,2,3,4,5], K=3, i=0 → middle=2
```

---

**🪜 Step 1.9: Window Size Formula**
```
Problem: Calculate current window size using pointers
Given: left pointer, right pointer
Formula: size = right - left + 1

Example: left=1, right=3 → size = 3-1+1 = 3

This is crucial for flexible windows!

Solution:
def window_size(left, right):
    return right - left + 1

# Practice: left=5, right=8 → size=4
```

---

**🪜 Step 1.10: Edge Cases**
```
Problem: Handle edge cases
1. Array smaller than K → No windows
2. K = 1 → Every element is a window
3. K = len(arr) → Only 1 window (entire array)

Solution:
def validate_window(arr, k):
    if len(arr) < k:
        return "No windows possible"
    if k == 1:
        return "Each element is a window"
    if k == len(arr):
        return "Only one window (entire array)"
    return f"{len(arr) - k + 1} windows"
```

---

### 🎓 STAIRCASE 2: Window Sum Operations (15 Micro-Steps)

**🪜 Step 2.1: Sum of First Window (Brute Force)**
```
Problem: Calculate sum of first K elements
Input: [1, 2, 3, 4, 5], K=3
Output: 6 (1+2+3)

Solution:
def sum_first_window(arr, k):
    return sum(arr[:k])

# Practice: [10, 20, 30, 40], K=2 → 30
```

---

**🪜 Step 2.2: Sum of All Windows (Brute Force)**
```
Problem: Calculate sum for each window separately
Input: [1, 2, 3, 4], K=2
Output: [3, 5, 7]

Time Complexity: O(N * K) - Can we improve?

Solution:
def all_window_sums_brute(arr, k):
    sums = []
    for i in range(len(arr) - k + 1):
        window_sum = sum(arr[i:i+k])  # O(K) each time
        sums.append(window_sum)
    return sums
```

---

**🪜 Step 2.3: The Sliding Concept - Visualize**
```
Problem: Understand what "slides" means

Array: [1, 2, 3, 4, 5], K=3

Window 1: [1, 2, 3] → sum = 6
           ↑     ↑
         remove add

Window 2: [2, 3, 4] → sum = 6 - 1 + 4 = 9
           ↑     ↑
         remove add

Key Insight: 
- Remove LEFT element (1)
- Add NEW RIGHT element (4)
- Result: 6 - 1 + 4 = 9

This is O(1) instead of recalculating O(K)!
```

---

**🪜 Step 2.4: Update Sum When Sliding**
```
Problem: Given current sum, update for next window
current_sum = 6 (from [1,2,3])
Next window: [2,3,4]

Formula: new_sum = current_sum - arr[left] + arr[right]
new_sum = 6 - 1 + 4 = 9 ✓

Practice:
- current_sum=12 (from [5,7]), next window [7,10]
  new_sum = 12 - 5 + 10 = 17

Solution:
def slide_window_sum(current_sum, remove_element, add_element):
    return current_sum - remove_element + add_element
```

---

**🪜 Step 2.5: Sum of All Windows (Optimized - Sliding)**
```
Problem: Use sliding technique for all windows
Input: [1, 2, 3, 4], K=2
Output: [3, 5, 7]

Time Complexity: O(N) - Much better!

Solution:
def all_window_sums_optimized(arr, k):
    if len(arr) < k:
        return []
    
    # Step 1: Calculate first window sum
    window_sum = sum(arr[:k])
    sums = [window_sum]
    
    # Step 2: Slide window
    for i in range(k, len(arr)):
        # Remove left element: arr[i-k]
        # Add right element: arr[i]
        window_sum = window_sum - arr[i-k] + arr[i]
        sums.append(window_sum)
    
    return sums

# Practice: [10, 20, 30, 40, 50], K=3
```

---

**🪜 Step 2.6: Maximum Window Sum** ⭐ **LeetCode Pattern**
```
Problem: Find maximum sum among all windows
Input: [2, 1, 5, 1, 3, 2], K=3
Output: 9 (from window [5, 1, 3])

LeetCode: Similar to #643 Maximum Average Subarray I

Solution:
def max_window_sum(arr, k):
    if len(arr) < k:
        return 0
    
    # First window
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    # Slide and track maximum
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum

# Practice: [1, 4, 2, 10, 23, 3, 1, 0, 20], K=4 → 39
```

---

**🪜 Step 2.7: Minimum Window Sum**
```
Problem: Find minimum sum among all windows
Input: [2, 1, 5, 1, 3, 2], K=3
Output: 6 (from window [2, 1, 3])

Solution:
def min_window_sum(arr, k):
    if len(arr) < k:
        return 0
    
    window_sum = sum(arr[:k])
    min_sum = window_sum
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        min_sum = min(min_sum, window_sum)
    
    return min_sum
```

---

**🪜 Step 2.8: Average of Each Window** 
```
Problem: Calculate average for each window
Input: [1, 3, 2, 6, -1, 4, 1, 8, 2], K=5
Output: [2.2, 2.8, 2.4, 3.6, 2.8]

LeetCode #643: Maximum Average Subarray I (find max average)

Solution:
def window_averages(arr, k):
    if len(arr) < k:
        return []
    
    averages = []
    window_sum = sum(arr[:k])
    averages.append(window_sum / k)
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        averages.append(window_sum / k)
    
    return averages
```

---

**🪜 Step 2.9: Maximum Average Subarray I** ⭐ **LeetCode #643**
```
Problem: Find maximum average of any K consecutive elements
Input: nums = [1,12,-5,-6,50,3], K=4
Output: 12.75 (from [12,-5,-6,50])

Solution:
def findMaxAverage(nums, k):
    window_sum = sum(nums[:k])
    max_sum = window_sum
    
    for i in range(k, len(nums)):
        window_sum = window_sum - nums[i-k] + nums[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum / k

# This is a direct LeetCode problem!
```

---

**🪜 Step 2.10: Count Windows with Sum > Target**
```
Problem: How many windows have sum greater than target?
Input: [2, 1, 5, 1, 3, 2], K=3, target=6
Output: 2 (windows [5,1,3]=9 and [1,3,2]=6 ... wait, that's equal)
Correct: Only [5,1,3]=9 > 6, so output=1

Solution:
def count_windows_above_target(arr, k, target):
    if len(arr) < k:
        return 0
    
    count = 0
    window_sum = sum(arr[:k])
    if window_sum > target:
        count += 1
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        if window_sum > target:
            count += 1
    
    return count
```

---

**🪜 Step 2.11: Windows with Exact Sum**
```
Problem: Count windows with sum exactly equal to target
Input: [1, 2, 1, 2, 1], K=2, target=3
Output: 3 (windows [1,2], [2,1], [2,1])

Solution:
def count_exact_sum(arr, k, target):
    if len(arr) < k:
        return 0
    
    count = 0
    window_sum = sum(arr[:k])
    if window_sum == target:
        count += 1
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        if window_sum == target:
            count += 1
    
    return count
```

---

**🪜 Step 2.12: Find Window Index with Maximum Sum**
```
Problem: Return START INDEX of window with max sum
Input: [2, 1, 5, 1, 3, 2], K=3
Output: 2 (window starting at index 2: [5,1,3]=9)

Solution:
def max_sum_window_index(arr, k):
    if len(arr) < k:
        return -1
    
    window_sum = sum(arr[:k])
    max_sum = window_sum
    max_index = 0
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        if window_sum > max_sum:
            max_sum = window_sum
            max_index = i - k + 1  # Start of current window
    
    return max_index
```

---

**🪜 Step 2.13: Sum Range Between L and R**
```
Problem: Sum of windows at indices L to R
Input: [1, 2, 3, 4, 5], K=2, L=1, R=2
Windows: [2,3]=5, [3,4]=7
Output: 12

Solution:
def sum_windows_in_range(arr, k, L, R):
    window_sum = sum(arr[:k])
    all_sums = [window_sum]
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        all_sums.append(window_sum)
    
    return sum(all_sums[L:R+1])
```

---

**🪜 Step 2.14: Cumulative Sum of Windows**
```
Problem: Cumulative sum of all window sums
Input: [1, 2, 3, 4], K=2
Window sums: [3, 5, 7]
Output: [3, 8, 15]

Solution:
def cumulative_window_sums(arr, k):
    window_sum = sum(arr[:k])
    sums = [window_sum]
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        sums.append(window_sum)
    
    # Cumulative
    cumulative = []
    total = 0
    for s in sums:
        total += s
        cumulative.append(total)
    
    return cumulative
```

---

**🪜 Step 2.15: Window Sum with Condition**
```
Problem: Only add to sum if element > threshold
Input: [5, 2, 8, 1, 9], K=3, threshold=3
Window [5,2,8]: sum only 5+8=13 (skip 2)
Window [2,8,1]: sum only 8=8
Window [8,1,9]: sum only 8+9=17

Solution:
def conditional_window_sum(arr, k, threshold):
    result = []
    
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        window_sum = sum(x for x in window if x > threshold)
        result.append(window_sum)
    
    return result
```

---

### 🎓 STAIRCASE 3: Window Max/Min Operations (10 Micro-Steps)

**🪜 Step 3.1: Maximum Element in Window**
```
Problem: Find max element in each window
Input: [1, 3, -1, -3, 5, 3, 6, 7], K=3
Output: [3, 3, 5, 5, 6, 7]

Solution (Brute Force):
def max_in_each_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window_max = max(arr[i:i+k])
        result.append(window_max)
    return result

# Time: O(N*K) - Can optimize with deque (later)
```

---

**🪜 Step 3.2: Minimum Element in Window**
```
Problem: Find min element in each window
Input: [1, 3, -1, -3, 5, 3], K=3
Output: [-1, -3, -3, -3]

Solution:
def min_in_each_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window_min = min(arr[i:i+k])
        result.append(window_min)
    return result
```

---

**🪜 Step 3.3: Sliding Window Maximum** ⭐ **LeetCode #239 (Hard)**
```
Problem: Optimized max in each window using deque
Input: nums = [1,3,-1,-3,5,3,6,7], K=3
Output: [3,3,5,5,6,7]

This is one of the hardest sliding window problems!
We'll build up to this...

Solution (Optimized with Deque - O(N)):
from collections import deque

def maxSlidingWindow(nums, k):
    if not nums or k == 0:
        return []
    
    dq = deque()  # Stores indices
    result = []
    
    for i in range(len(nums)):
        # Remove elements outside window
        if dq and dq[0] < i - k + 1:
            dq.popleft()
        
        # Remove smaller elements (they're useless)
        while dq and nums[dq[-1]] < nums[i]:
            dq.pop()
        
        dq.append(i)
        
        # Add to result once window is full
        if i >= k - 1:
            result.append(nums[dq[0]])
    
    return result
```

---

**🪜 Step 3.4: Count of Max in Window**
```
Problem: How many times does max element appear in window?
Input: [1, 3, 3, -1, 5], K=3
Window [1,3,3]: max=3, count=2
Window [3,3,-1]: max=3, count=2
Window [3,-1,5]: max=5, count=1

Solution:
def count_max_in_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        window_max = max(window)
        count = window.count(window_max)
        result.append(count)
    return result
```

---

**🪜 Step 3.5: Max - Min in Each Window**
```
Problem: Find difference between max and min in each window
Input: [1, 3, -1, -3, 5], K=3
Window [1,3,-1]: max=3, min=-1, diff=4
Window [3,-1,-3]: max=3, min=-3, diff=6
Window [-1,-3,5]: max=5, min=-3, diff=8

Solution:
def max_min_diff_windows(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        diff = max(window) - min(window)
        result.append(diff)
    return result
```

---

**🪜 Step 3.6: First Maximum in Window**
```
Problem: Index of first occurrence of max in window
Input: [1, 3, 3, 2], K=3
Window [1,3,3]: max=3, first at index 1

Solution:
def first_max_index_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        window_max = max(window)
        first_index = i + window.index(window_max)
        result.append(first_index)
    return result
```

---

**🪜 Step 3.7: Windows Where Max > Threshold**
```
Problem: Count windows where maximum exceeds threshold
Input: [1, 5, 3, 8, 2], K=2, threshold=4
Windows: [1,5]=5>4 ✓, [5,3]=5>4 ✓, [3,8]=8>4 ✓, [8,2]=8>4 ✓
Output: 4

Solution:
def count_windows_max_above(arr, k, threshold):
    count = 0
    for i in range(len(arr) - k + 1):
        if max(arr[i:i+k]) > threshold:
            count += 1
    return count
```

---

**🪜 Step 3.8: Windows with Same Max and Min**
```
Problem: Find windows where all elements are equal
Input: [1, 1, 1, 2, 2, 2, 3], K=3
Window [1,1,1]: max=min=1 ✓
Window [2,2,2]: max=min=2 ✓

Solution:
def windows_all_equal(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        if max(window) == min(window):
            result.append(i)
    return result
```

---

**🪜 Step 3.9: Product of Max and Min**
```
Problem: Multiply max and min of each window
Input: [2, 5, 1, 8, 3], K=3
Window [2,5,1]: max=5, min=1, product=5
Window [5,1,8]: max=8, min=1, product=8
Window [1,8,3]: max=8, min=1, product=8

Solution:
def product_max_min(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        product = max(window) * min(window)
        result.append(product)
    return result
```

---

**🪜 Step 3.10: Median of Each Window** (Advanced)
```
Problem: Find median element in each window
Input: [1, 3, -1, -3, 5, 3, 6], K=3
Window [1,3,-1]: sorted=[-1,1,3], median=1
Window [3,-1,-3]: sorted=[-3,-1,3], median=-1

Solution:
def median_windows(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = sorted(arr[i:i+k])
        median_idx = k // 2
        result.append(window[median_idx])
    return result
```

---

### 🎓 STAIRCASE 4: Window with Conditions (15 Micro-Steps)

**🪜 Step 4.1: Count Positive Numbers in Window**
```
Problem: How many positive numbers in each window?
Input: [1, -2, 3, -4, 5, 6], K=3
Window [1,-2,3]: count=2
Window [-2,3,-4]: count=1
Window [3,-4,5]: count=2

Solution:
def count_positives_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        count = sum(1 for x in window if x > 0)
        result.append(count)
    return result
```

---

**🪜 Step 4.2: Count Even Numbers in Window**
```
Problem: Count even numbers in each window
Input: [1, 2, 3, 4, 5, 6], K=3
Window [1,2,3]: count=1 (only 2)
Window [2,3,4]: count=2 (2 and 4)
Window [3,4,5]: count=1 (only 4)

Solution:
def count_evens_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        count = sum(1 for x in arr[i:i+k] if x % 2 == 0)
        result.append(count)
    return result
```

---

**🪜 Step 4.3: All Positive Window**
```
Problem: Check if all elements in window are positive
Input: [1, 2, -3, 4, 5], K=2
Window [1,2]: all positive? YES
Window [2,-3]: all positive? NO
Window [-3,4]: all positive? NO

Solution:
def all_positive_windows(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        all_positive = all(x > 0 for x in arr[i:i+k])
        result.append(all_positive)
    return result
```

---

**🪜 Step 4.4: Windows with At Least One Negative**
```
Problem: Does window contain at least one negative?
Input: [1, 2, -3, 4, 5], K=2
Window [1,2]: NO
Window [2,-3]: YES
Window [-3,4]: YES

Solution:
def has_negative_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        has_neg = any(x < 0 for x in arr[i:i+k])
        result.append(has_neg)
    return result
```

---

**🪜 Step 4.5: First Negative in Each Window** ⭐ **Common Interview**
```
Problem: Find first negative number in each window (0 if none)
Input: [12, -1, -7, 8, -15, 30, 16, 28], K=3
Window [12,-1,-7]: first negative = -1
Window [-1,-7,8]: first negative = -1
Window [-7,8,-15]: first negative = -7
Window [8,-15,30]: first negative = -15
Window [-15,30,16]: first negative = -15
Window [30,16,28]: first negative = 0 (none)

Output: [-1, -1, -7, -15, -15, 0]

Solution:
def first_negative_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        first_neg = next((x for x in window if x < 0), 0)
        result.append(first_neg)
    return result

# This is a VERY common interview question!
```

---

**🪜 Step 4.6: Count Distinct Elements** ⭐ **Common Pattern**
```
Problem: Count unique elements in each window
Input: [1, 2, 1, 3, 4, 2, 3], K=4
Window [1,2,1,3]: distinct = {1,2,3} = 3
Window [2,1,3,4]: distinct = {1,2,3,4} = 4
Window [1,3,4,2]: distinct = {1,2,3,4} = 4
Window [3,4,2,3]: distinct = {2,3,4} = 3

Output: [3, 4, 4, 3]

Solution:
def count_distinct_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        distinct_count = len(set(window))
        result.append(distinct_count)
    return result

# Can optimize with sliding hash map (flexible window)
```

---

**🪜 Step 4.7: Window with All Distinct Elements**
```
Problem: Check if all elements in window are unique
Input: [1, 2, 3, 2, 4], K=3
Window [1,2,3]: all distinct? YES
Window [2,3,2]: all distinct? NO (2 repeats)
Window [3,2,4]: all distinct? YES

Solution:
def all_distinct_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        all_distinct = len(window) == len(set(window))
        result.append(all_distinct)
    return result
```

---

**🪜 Step 4.8: Most Frequent Element in Window**
```
Problem: Find element with highest frequency in each window
Input: [1, 2, 2, 3, 3, 3], K=3
Window [1,2,2]: most frequent = 2 (appears 2 times)
Window [2,2,3]: most frequent = 2
Window [2,3,3]: most frequent = 3
Window [3,3,3]: most frequent = 3

Solution:
from collections import Counter

def most_frequent_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        counter = Counter(window)
        most_common = counter.most_common(1)[0][0]
        result.append(most_common)
    return result
```

---

**🪜 Step 4.9: Count Duplicates in Window**
```
Problem: Count how many elements appear more than once
Input: [1, 2, 2, 3, 3, 4], K=4
Window [1,2,2,3]: duplicates = 1 (only 2 repeats)
Window [2,2,3,3]: duplicates = 2 (2 and 3 repeat)
Window [2,3,3,4]: duplicates = 1 (only 3 repeats)

Solution:
from collections import Counter

def count_duplicates_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        counter = Counter(window)
        duplicates = sum(1 for count in counter.values() if count > 1)
        result.append(duplicates)
    return result
```

---

**🪜 Step 4.10: Window with Target Element**
```
Problem: Does window contain target element?
Input: [1, 2, 3, 4, 5], K=3, target=3
Window [1,2,3]: contains 3? YES
Window [2,3,4]: contains 3? YES
Window [3,4,5]: contains 3? YES

Solution:
def window_contains_target(arr, k, target):
    result = []
    for i in range(len(arr) - k + 1):
        contains = target in arr[i:i+k]
        result.append(contains)
    return result
```

---

**🪜 Step 4.11: Count Zeros in Window**
```
Problem: Count zero elements in each window
Input: [1, 0, 0, 1, 1, 0], K=3
Window [1,0,0]: zeros=2
Window [0,0,1]: zeros=2
Window [0,1,1]: zeros=1
Window [1,1,0]: zeros=1

Solution:
def count_zeros_window(arr, k):
    result = []
    for i in range(len(arr) - k + 1):
        zeros = arr[i:i+k].count(0)
        result.append(zeros)
    return result
```

---

**🪜 Step 4.12: Max Consecutive Ones** ⭐ **LeetCode #1004**
```
Problem: Longest sequence of 1s after flipping at most K zeros
Input: [1,1,1,0,0,0,1,1,1,1,0], K=2
Output: 6

This transitions us to FLEXIBLE windows!

Solution (This needs flexible window - preview):
def longestOnes(arr, k):
    left = 0
    zero_count = 0
    max_length = 0
    
    for right in range(len(arr)):
        if arr[right] == 0:
            zero_count += 1
        
        while zero_count > k:
            if arr[left] == 0:
                zero_count -= 1
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length

# LeetCode #1004: Max Consecutive Ones III
```

---

**🪜 Step 4.13: Window Product Less Than K** 
```
Problem: Check if product of window < K
Input: [2, 3, 1, 4], K=10, window_size=2
Window [2,3]: product=6 < 10? YES
Window [3,1]: product=3 < 10? YES
Window [1,4]: product=4 < 10? YES

Solution:
def product_less_than_k(arr, k, window_size):
    result = []
    for i in range(len(arr) - window_size + 1):
        window = arr[i:i+window_size]
        product = 1
        for num in window:
            product *= num
        result.append(product < k)
    return result
```

---

**🪜 Step 4.14: Vowels in String Window**
```
Problem: Count vowels in each K-character window
Input: s = "abciiidef", K=3
Window "abc": vowels=1 (a)
Window "bci": vowels=1 (i)
Window "cii": vowels=2 (i, i)
Window "iii": vowels=3 (i, i, i)

Output: [1, 1, 2, 3, 2, 1, 1]

Solution:
def count_vowels_window(s, k):
    vowels = set('aeiouAEIOU')
    result = []
    
    for i in range(len(s) - k + 1):
        window = s[i:i+k]
        count = sum(1 for c in window if c in vowels)
        result.append(count)
    
    return result
```

---

**🪜 Step 4.15: Maximum Vowels in Substring** ⭐ **LeetCode #1456**
```
Problem: Max vowels in any K-length substring
Input: s = "abciiidef", K=3
Output: 3 (from "iii")

Solution:
def maxVowels(s, k):
    vowels = set('aeiouAEIOU')
    
    # First window
    current_vowels = sum(1 for c in s[:k] if c in vowels)
    max_vowels = current_vowels
    
    # Slide
    for i in range(k, len(s)):
        # Remove left character
        if s[i-k] in vowels:
            current_vowels -= 1
        # Add right character
        if s[i] in vowels:
            current_vowels += 1
        
        max_vowels = max(max_vowels, current_vowels)
    
    return max_vowels

# LeetCode #1456: Maximum Number of Vowels in Substring
```

---

## 🟠 PART 2: FLEXIBLE/DYNAMIC WINDOW (VARIABLE SIZE)

### **Core Pattern:**
```python
# Template for Flexible Window
left = 0
for right in range(len(arr)):
    # EXPAND: Add arr[right] to window
    window_data += arr[right]
    
    # SHRINK: While condition violated
    while condition_invalid:
        window_data -= arr[left]
        left += 1
    
    # UPDATE: Track optimal result
    result = optimize(result, right - left + 1)
```

---

### 🎓 STAIRCASE 5: Flexible Window Basics (15 Micro-Steps)

**🪜 Step 5.1: Understanding Flexible Window**
```
Concept: Window size CHANGES based on condition

Example: Find smallest subarray with sum >= 7
[2, 1, 5, 2, 3, 2]

Start: left=0, right=0, sum=2
Expand: right=1, sum=3
Expand: right=2, sum=8 (>= 7!) ← First valid window
Shrink: left=1, sum=6 (< 7)
Expand: right=3, sum=8 (>= 7!) ← Found smaller window
...

Key: Expand to meet condition, shrink to optimize
```

---

**🪜 Step 5.2: Expand Only (No Shrink)**
```
Problem: Keep expanding until sum >= target, then stop
Input: [1, 2, 3, 4, 5], target=7
Output: Window [1, 2, 3, 4] (sum=10)

Solution:
def expand_until_target(arr, target):
    window_sum = 0
    
    for right in range(len(arr)):
        window_sum += arr[right]
        
        if window_sum >= target:
            return arr[:right+1]
    
    return arr  # If target not reached
```

---

**🪜 Step 5.3: Expand and Track Window Size**
```
Problem: Track window size as we expand
Input: [1, 2, 3, 4, 5]
Output: [1, 2, 3, 4, 5] (sizes at each step)

Solution:
def track_window_size(arr):
    sizes = []
    left = 0
    
    for right in range(len(arr)):
        current_size = right - left + 1
        sizes.append(current_size)
    
    return sizes

# Result: [1, 2, 3, 4, 5]
```

---

**🪜 Step 5.4: Shrink from Left**
```
Problem: Remove elements from left until sum < target
Input: [5, 10, 15, 20], current_sum=50, target=30
Output: After shrinking, sum=35 (removed 5, 10)

Solution:
def shrink_until_below(arr, target):
    window_sum = sum(arr)
    left = 0
    
    while window_sum >= target and left < len(arr):
        window_sum -= arr[left]
        left += 1
        print(f"After removing arr[{left-1}], sum={window_sum}")
    
    return left  # Number of elements removed
```

---

**🪜 Step 5.5: Expand-Shrink Basic Pattern**
```
Problem: Implement basic expand-shrink loop
Input: [1, 2, 3, 4, 5], target_sum=7

Trace:
right=0: sum=1, window=[1]
right=1: sum=3, window=[1,2]
right=2: sum=6, window=[1,2,3]
right=3: sum=10 (>7), shrink left, sum=9, sum=7 ← Found!

Solution:
def basic_expand_shrink(arr, target):
    window_sum = 0
    left = 0
    
    for right in range(len(arr)):
        window_sum += arr[right]  # Expand
        
        # Shrink while over target
        while window_sum > target and left <= right:
            window_sum -= arr[left]
            left += 1
    
    return window_sum
```

---

**🪜 Step 5.6: Smallest Subarray Sum >= S** ⭐ **LeetCode #209**
```
Problem: Find length of smallest subarray with sum >= S
Input: arr = [2,3,1,2,4,3], S = 7
Output: 2 (subarray [4,3])

Solution:
def minSubArrayLen(target, nums):
    min_length = float('inf')
    window_sum = 0
    left = 0
    
    for right in range(len(nums)):
        window_sum += nums[right]  # Expand
        
        # Shrink while condition met
        while window_sum >= target:
            min_length = min(min_length, right - left + 1)
            window_sum -= nums[left]
            left += 1
    
    return min_length if min_length != float('inf') else 0

# LeetCode #209: Minimum Size Subarray Sum
```

---

**🪜 Step 5.7: Longest Subarray Sum <= K**
```
Problem: Find longest subarray with sum at most K
Input: [1, 2, 3, 4, 5], K=8
Output: 3 (subarray [1,2,3] or [1,2,3] sum=6)

Solution:
def longest_sum_at_most_k(arr, K):
    max_length = 0
    window_sum = 0
    left = 0
    
    for right in range(len(arr)):
        window_sum += arr[right]
        
        # Shrink if sum exceeds K
        while window_sum > K:
            window_sum -= arr[left]
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

---

**🪜 Step 5.8: Count Subarrays with Sum Exactly K**
```
Problem: Count subarrays with sum equal to K
Input: [1, 2, 1, 2, 1], K=3
Output: 4

Note: This needs PREFIX SUM, not sliding window!

Solution:
def subarraySum(nums, k):
    count = 0
    prefix_sum = 0
    sum_map = {0: 1}
    
    for num in nums:
        prefix_sum += num
        
        if prefix_sum - k in sum_map:
            count += sum_map[prefix_sum - k]
        
        sum_map[prefix_sum] = sum_map.get(prefix_sum, 0) + 1
    
    return count

# LeetCode #560: Subarray Sum Equals K
```

---

**🪜 Step 5.9: Max Length with Sum At Most K**
```
Problem: Maximum length subarray with sum <= K
Input: [1, 2, 3, 1, 1, 1, 1], K=5
Output: 5 (subarray [1,1,1,1,1])

Solution:
def max_length_sum_k(arr, K):
    max_len = 0
    window_sum = 0
    left = 0
    
    for right in range(len(arr)):
        window_sum += arr[right]
        
        while window_sum > K:
            window_sum -= arr[left]
            left += 1
        
        max_len = max(max_len, right - left + 1)
    
    return max_len
```

---

**🪜 Step 5.10: Window with Exactly K Odd Numbers**
```
Problem: Longest subarray with exactly K odd numbers
Input: [1, 1, 2, 1, 1], K=3
Output: 5 (entire array has 4 odd... wait, let me recount)
Actually [1,1,2,1,1] has 4 odd numbers

Let's use: [2, 2, 1, 3, 5, 2], K=2
Output: 5 (subarray [1,3,5,2] has exactly 2 odd: 1,3 or [2,1,3,5] has 1,3,5=3 odd)

Solution:
def longest_k_odds(arr, K):
    max_len = 0
    odd_count = 0
    left = 0
    
    for right in range(len(arr)):
        if arr[right] % 2 == 1:
            odd_count += 1
        
        while odd_count > K:
            if arr[left] % 2 == 1:
                odd_count -= 1
            left += 1
        
        if odd_count == K:
            max_len = max(max_len, right - left + 1)
    
    return max_len
```

---

**🪜 Step 5.11: Subarrays with Product < K** ⭐ **LeetCode #713**
```
Problem: Count subarrays where product < K
Input: nums = [10,5,2,6], K = 100
Output: 8

Subarrays: [10],[5],[2],[6],[10,5],[5,2],[2,6],[5,2,6]

Solution:
def numSubarrayProductLessThanK(nums, k):
    if k <= 1:
        return 0
    
    count = 0
    product = 1
    left = 0
    
    for right in range(len(nums)):
        product *= nums[right]
        
        while product >= k:
            product //= nums[left]
            left += 1
        
        # All subarrays ending at right
        count += right - left + 1
    
    return count

# LeetCode #713: Subarray Product Less Than K
```

---

**🪜 Step 5.12: Longest Ones After K Flips** ⭐ **LeetCode #1004**
```
Problem: Longest sequence of 1s after flipping K zeros
Input: [1,1,1,0,0,0,1,1,1,1,0], K=2
Output: 6 (flip two zeros to get [1,1,1,1,1,1])

Solution:
def longestOnes(nums, k):
    left = 0
    zero_count = 0
    max_length = 0
    
    for right in range(len(nums)):
        if nums[right] == 0:
            zero_count += 1
        
        # Shrink if too many zeros
        while zero_count > k:
            if nums[left] == 0:
                zero_count -= 1
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length

# LeetCode #1004: Max Consecutive Ones III
```

---

**🪜 Step 5.13: Count Nice Subarrays** ⭐ **LeetCode #1248**
```
Problem: Count subarrays with exactly K odd numbers
Input: nums = [1,1,2,1,1], K = 3
Output: 2 (subarrays [1,2,1,1] and [1,1,2,1])

Technique: at_most(K) - at_most(K-1) = exactly(K)

Solution:
def numberOfSubarrays(nums, k):
    def at_most_k(k):
        count = 0
        odd_count = 0
        left = 0
        
        for right in range(len(nums)):
            if nums[right] % 2 == 1:
                odd_count += 1
            
            while odd_count > k:
                if nums[left] % 2 == 1:
                    odd_count -= 1
                left += 1
            
            count += right - left + 1
        
        return count
    
    return at_most_k(k) - at_most_k(k - 1)

# LeetCode #1248: Count Number of Nice Subarrays
```

---

**🪜 Step 5.14: Longest Subarray After Deleting One Element** ⭐ **LeetCode #1493**
```
Problem: Longest subarray of 1s after deleting one element
Input: [1,1,0,1]
Output: 3 (delete 0, get [1,1,1])

Input: [0,1,1,1,0,1,1,0,1]
Output: 5 (delete middle 0, get [1,1,1,1,1])

Solution:
def longestSubarray(nums):
    left = 0
    zero_count = 0
    max_length = 0
    
    for right in range(len(nums)):
        if nums[right] == 0:
            zero_count += 1
        
        # At most 1 zero (the one we delete)
        while zero_count > 1:
            if nums[left] == 0:
                zero_count -= 1
            left += 1
        
        # Subtract 1 because we must delete one element
        max_length = max(max_length, right - left)
    
    return max_length

# LeetCode #1493: Longest Subarray of 1s After Deleting One
```

---

**🪜 Step 5.15: Minimum Window with Sum >= Target**
```
Problem: Smallest window with sum at least target
Input: [2, 3, 1, 2, 4, 3], target=7
Output: 2 (subarray [4,3]=7)

This is same as Step 5.6 - LeetCode #209!

Review the solution above.
```

---

### 🎓 STAIRCASE 6: String Windows (20 Micro-Steps)

**🪜 Step 6.1: Character Frequency in Window**
```
Problem: Track character frequencies in a string window
Input: s = "abc", window_size=2
Window "ab": {'a':1, 'b':1}
Window "bc": {'b':1, 'c':1}

Solution:
from collections import defaultdict

def char_freq_windows(s, k):
    result = []
    
    for i in range(len(s) - k + 1):
        window = s[i:i+k]
        freq = defaultdict(int)
        for char in window:
            freq[char] += 1
        result.append(dict(freq))
    
    return result
```

---

**🪜 Step 6.2: Count Distinct Characters in Window**
```
Problem: Count unique characters in each window
Input: s = "aabbcc", K=3
Window "aab": distinct=2
Window "abb": distinct=2
Window "bbc": distinct=2
Window "bcc": distinct=2

Solution:
def distinct_chars_window(s, k):
    result = []
    
    for i in range(len(s) - k + 1):
        window = s[i:i+k]
        distinct = len(set(window))
        result.append(distinct)
    
    return result
```

---

**🪜 Step 6.3: Longest Substring with K Distinct** ⭐ **LeetCode #340 (Premium)**
```
Problem: Longest substring with at most K distinct characters
Input: s = "eceba", K = 2
Output: 3 (substring "ece" or "eba")

Solution:
def lengthOfLongestSubstringKDistinct(s, k):
    if k == 0:
        return 0
    
    char_count = {}
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        # Expand
        char_count[s[right]] = char_count.get(s[right], 0) + 1
        
        # Shrink
        while len(char_count) > k:
            char_count[s[left]] -= 1
            if char_count[s[left]] == 0:
                del char_count[s[left]]
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length

# LeetCode #340: Longest Substring with At Most K Distinct
```

---

**🪜 Step 6.4: Longest Substring with Exactly K Distinct**
```
Problem: Exactly K distinct (not "at most")
Input: s = "aabbcc", K = 2
Output: 4 (substring "aabb" or "bbcc")

Technique: at_most(K) - at_most(K-1)

Solution:
def longest_exactly_k_distinct(s, k):
    def at_most_k(k):
        char_count = {}
        left = 0
        max_len = 0
        
        for right in range(len(s)):
            char_count[s[right]] = char_count.get(s[right], 0) + 1
            
            while len(char_count) > k:
                char_count[s[left]] -= 1
                if char_count[s[left]] == 0:
                    del char_count[s[left]]
                left += 1
            
            max_len = max(max_len, right - left + 1)
        
        return max_len
    
    return at_most_k(k) - at_most_k(k - 1)
```

---

**🪜 Step 6.5: Longest Substring Without Repeating** ⭐ **LeetCode #3**
```
Problem: Longest substring with all unique characters
Input: s = "abcabcbb"
Output: 3 (substring "abc")

Input: s = "bbbbb"
Output: 1 (substring "b")

Solution:
def lengthOfLongestSubstring(s):
    char_set = set()
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        # Shrink until character is unique
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        
        char_set.add(s[right])
        max_length = max(max_length, right - left + 1)
    
    return max_length

# LeetCode #3: Longest Substring Without Repeating Characters
# This is one of the MOST ASKED interview questions!
```

---

**🪜 Step 6.6: Character Replacement** ⭐ **LeetCode #424**
```
Problem: Longest substring with same letter after K replacements
Input: s = "AABABBA", K = 1
Output: 4 (substring "AABA", replace one B)

Solution:
def characterReplacement(s, k):
    char_count = {}
    left = 0
    max_freq = 0
    max_length = 0
    
    for right in range(len(s)):
        char_count[s[right]] = char_count.get(s[right], 0) + 1
        max_freq = max(max_freq, char_count[s[right]])
        
        # Window size - most frequent > K means invalid
        while (right - left + 1) - max_freq > k:
            char_count[s[left]] -= 1
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length

# LeetCode #424: Longest Repeating Character Replacement
```

---

**🪜 Step 6.7: Minimum Window Substring** ⭐ **LeetCode #76 (Hard)**
```
Problem: Smallest substring containing all characters of pattern
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"

This is a HARD problem - let's build it step by step!

Solution:
def minWindow(s, t):
    if not s or not t:
        return ""
    
    # Character counts in pattern
    pattern_count = {}
    for char in t:
        pattern_count[char] = pattern_count.get(char, 0) + 1
    
    required = len(pattern_count)  # Unique chars needed
    formed = 0  # Unique chars currently matched
    
    window_counts = {}
    left = 0
    min_length = float('inf')
    min_left = 0
    
    for right in range(len(s)):
        # Expand
        char = s[right]
        window_counts[char] = window_counts.get(char, 0) + 1
        
        # Check if this character's frequency matches
        if char in pattern_count and window_counts[char] == pattern_count[char]:
            formed += 1
        
        # Shrink
        while formed == required and left <= right:
            # Update result
            if right - left + 1 < min_length:
                min_length = right - left + 1
                min_left = left
            
            # Remove left character
            char = s[left]
            window_counts[char] -= 1
            if char in pattern_count and window_counts[char] < pattern_count[char]:
                formed -= 1
            
            left += 1
    
    return s[min_left:min_left + min_length] if min_length != float('inf') else ""

# LeetCode #76: Minimum Window Substring
# One of the HARDEST sliding window problems!
```

---

**🪜 Step 6.8: Permutation in String** ⭐ **LeetCode #567**
```
Problem: Check if s2 contains permutation of s1
Input: s1 = "ab", s2 = "eidbaooo"
Output: True (s2 contains "ba" which is permutation of "ab")

Solution:
def checkInclusion(s1, s2):
    if len(s1) > len(s2):
        return False
    
    s1_count = {}
    window_count = {}
    
    for char in s1:
        s1_count[char] = s1_count.get(char, 0) + 1
    
    # Fixed window size = len(s1)
    window_size = len(s1)
    
    # First window
    for i in range(window_size):
        char = s2[i]
        window_count[char] = window_count.get(char, 0) + 1
    
    if window_count == s1_count:
        return True
    
    # Slide window
    for i in range(window_size, len(s2)):
        # Add new character
        char = s2[i]
        window_count[char] = window_count.get(char, 0) + 1
        
        # Remove old character
        old_char = s2[i - window_size]
        window_count[old_char] -= 1
        if window_count[old_char] == 0:
            del window_count[old_char]
        
        if window_count == s1_count:
            return True
    
    return False

# LeetCode #567: Permutation in String
```

---

**🪜 Step 6.9: Find All Anagrams** ⭐ **LeetCode #438**
```
Problem: Find all start indices of anagrams of p in s
Input: s = "cbaebabacd", p = "abc"
Output: [0, 6] (substrings "cba" and "bac")

Solution:
def findAnagrams(s, p):
    if len(p) > len(s):
        return []
    
    p_count = {}
    window_count = {}
    result = []
    
    for char in p:
        p_count[char] = p_count.get(char, 0) + 1
    
    window_size = len(p)
    
    # First window
    for i in range(window_size):
        char = s[i]
        window_count[char] = window_count.get(char, 0) + 1
    
    if window_count == p_count:
        result.append(0)
    
    # Slide
    for i in range(window_size, len(s)):
        # Add new
        window_count[s[i]] = window_count.get(s[i], 0) + 1
        
        # Remove old
        old_char = s[i - window_size]
        window_count[old_char] -= 1
        if window_count[old_char] == 0:
            del window_count[old_char]
        
        if window_count == p_count:
            result.append(i - window_size + 1)
    
    return result

# LeetCode #438: Find All Anagrams in a String
```

---

**🪜 Step 6.10: Longest Substring with At Most 2 Distinct** ⭐ **LeetCode #159**
```
Problem: Longest substring with at most 2 distinct characters
Input: s = "eceba"
Output: 3 ("ece")

This is just K=2 version of Step 6.3!

Solution:
def lengthOfLongestSubstringTwoDistinct(s):
    return lengthOfLongestSubstringKDistinct(s, 2)

# Use solution from Step 6.3 with K=2
# LeetCode #159: Longest Substring with At Most Two Distinct
```

---

**🪜 Step 6.11: Longest Palindromic Substring** (Not Window!)
```
Note: This is NOT a sliding window problem!
Use expand-around-center or DP instead.

LeetCode #5: Longest Palindromic Substring
(Different technique - included for comparison)
```

---

**🪜 Step 6.12: Fruits Into Baskets** ⭐ **LeetCode #904**
```
Problem: Maximum fruits you can collect (at most 2 types)
Input: fruits = [1,2,1]
Output: 3

Input: fruits = [0,1,2,2]
Output: 3 (collect [1,2,2])

This is SAME as longest substring with K=2 distinct!

Solution:
def totalFruit(fruits):
    fruit_count = {}
    left = 0
    max_fruits = 0
    
    for right in range(len(fruits)):
        fruit_count[fruits[right]] = fruit_count.get(fruits[right], 0) + 1
        
        while len(fruit_count) > 2:
            fruit_count[fruits[left]] -= 1
            if fruit_count[fruits[left]] == 0:
                del fruit_count[fruits[left]]
            left += 1
        
        max_fruits = max(max_fruits, right - left + 1)
    
    return max_fruits

# LeetCode #904: Fruit Into Baskets
```

---

**🪜 Step 6.13: Repeated DNA Sequences** ⭐ **LeetCode #187**
```
Problem: Find all 10-letter sequences that appear more than once
Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
Output: ["AAAAACCCCC", "CCCCCAAAAA"]

Solution:
def findRepeatedDnaSequences(s):
    if len(s) < 10:
        return []
    
    seen = set()
    repeated = set()
    
    for i in range(len(s) - 9):
        sequence = s[i:i+10]
        if sequence in seen:
            repeated.add(sequence)
        seen.add(sequence)
    
    return list(repeated)

# LeetCode #187: Repeated DNA Sequences
# Fixed window of size 10
```

---

**🪜 Step 6.14: Longest Substring of All Vowels** ⭐ **LeetCode #1371**
```
Problem: Longest substring containing all vowels (a,e,i,o,u)
Input: s = "aeiaaioooaaaeee"
Output: 10 (substring "aaioooaaae" starting index 4)

Wait, that doesn't contain all vowels...
Actually: Need substring with ALL five vowels present

Solution:
def longestSubstring(s):
    vowels = {'a', 'e', 'i', 'o', 'u'}
    vowel_count = {v: 0 for v in vowels}
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        if s[right] in vowels:
            vowel_count[s[right]] += 1
        
        # Shrink while all vowels present
        while all(count > 0 for count in vowel_count.values()):
            max_length = max(max_length, right - left + 1)
            if s[left] in vowels:
                vowel_count[s[left]] -= 1
            left += 1
    
    return max_length

# LeetCode #1371: Find Longest Substrings (variant)
```

---

**🪜 Step 6.15: Substring with Concatenation** ⭐ **LeetCode #30 (Hard)**
```
Problem: Find all start indices where concatenation of words appears
Input: s = "barfoothefoobarman", words = ["foo","bar"]
Output: [0, 9]

This is VERY hard - uses fixed window + hashmap

Solution:
def findSubstring(s, words):
    if not s or not words:
        return []
    
    word_len = len(words[0])
    word_count = len(words)
    total_len = word_len * word_count
    
    word_map = {}
    for word in words:
        word_map[word] = word_map.get(word, 0) + 1
    
    result = []
    
    for i in range(len(s) - total_len + 1):
        seen = {}
        j = 0
        
        while j < word_count:
            word_start = i + j * word_len
            word = s[word_start:word_start + word_len]
            
            if word not in word_map:
                break
            
            seen[word] = seen.get(word, 0) + 1
            
            if seen[word] > word_map[word]:
                break
            
            j += 1
        
        if j == word_count:
            result.append(i)
    
    return result

# LeetCode #30: Substring with Concatenation of All Words
```

---

**🪜 Step 6.16-6.20: Advanced String Window Problems**

**🪜 Step 6.16**: Binary Subarrays With Sum (LeetCode #930)
**🪜 Step 6.17**: Get Equal Substrings Within Budget (LeetCode #1208)  
**🪜 Step 6.18**: Max Consecutive Ones II (LeetCode #487)
**🪜 Step 6.19**: Longest Turbulent Subarray (LeetCode #978)
**🪜 Step 6.20**: Grumpy Bookstore Owner (LeetCode #1052)

(Solutions similar to patterns above - practice these on LeetCode!)

---

## 🎯 MASTERY CHECKLIST

### Fixed Window Mastery:
- [ ] Can calculate sum using sliding technique
- [ ] Know when to use fixed vs flexible window
- [ ] Can optimize from O(N*K) to O(N)
- [ ] Handle edge cases (K > N, K=1, K=N)
- [ ] Track max/min/average in windows

### Flexible Window Mastery:
- [ ] Understand expand-shrink pattern
- [ ] Know when to use "at most K" technique
- [ ] Can track window state (sum, count, frequency)
- [ ] Handle string windows with hashmaps
- [ ] Solve minimum and maximum problems

### Pattern Recognition:
- [ ] Identify fixed size from problem (given K)
- [ ] Identify flexible from "smallest/longest"
- [ ] Recognize "at most K" vs "exactly K"
- [ ] Know when to use frequency maps
- [ ] Understand "sliding" optimization

---

## 📊 LEETCODE PROBLEMS SUMMARY

### Easy:
1. **#643** - Maximum Average Subarray I (Fixed Window)
2. **#1456** - Maximum Vowels in Substring (Fixed Window)

### Medium:
3. **#3** - Longest Substring Without Repeating (Flexible) ⭐ MOST ASKED
4. **#209** - Minimum Size Subarray Sum (Flexible)
5. **#424** - Longest Repeating Character Replacement (Flexible)
6. **#438** - Find All Anagrams in a String (Fixed)
7. **#567** - Permutation in String (Fixed)
8. **#713** - Subarray Product Less Than K (Flexible)
9. **#904** - Fruit Into Baskets (Flexible)
10. **#1004** - Max Consecutive Ones III (Flexible)
11. **#1248** - Count Nice Subarrays (Flexible)
12. **#1493** - Longest Subarray After Deleting One (Flexible)

### Hard:
13. **#76** - Minimum Window Substring (Flexible) ⭐ HARDEST
14. **#239** - Sliding Window Maximum (Fixed with Deque)
15. **#30** - Substring with Concatenation (Fixed + HashMap)

### Premium:
16. **#159** - Longest Substring with At Most 2 Distinct
17. **#340** - Longest Substring with At Most K Distinct

---

## 🚀 PRACTICE SCHEDULE

### Week 1: Fixed Window Foundation
- **Day 1-2**: Staircase 1 (Window Basics)
- **Day 3-4**: Staircase 2 (Sum Operations)
- **Day 5**: Staircase 3 (Max/Min)
- **Weekend**: LeetCode #643, #1456

### Week 2: Flexible Window Introduction
- **Day 1-2**: Staircase 5 (Flexible Basics)
- **Day 3-4**: LeetCode #209, #713, #1004
- **Day 5**: Review and mixed practice
- **Weekend**: LeetCode #1248, #1493

### Week 3: String Windows
- **Day 1-2**: Staircase 6 (String Basics)
- **Day 3**: LeetCode #3, #424 ⭐
- **Day 4**: LeetCode #438, #567
- **Day 5**: LeetCode #904, review
- **Weekend**: Mixed practice

### Week 4: Advanced + Hard Problems
- **Day 1-2**: LeetCode #76 (Minimum Window) ⭐
- **Day 3-4**: LeetCode #239 (Sliding Max with Deque)
- **Day 5**: LeetCode #30
- **Weekend**: Speed solve previous problems

---

## 💡 KEY INSIGHTS

### When to Use Fixed Window:
- Problem gives you exact window size K
- Need to check ALL windows of size K
- Examples: "maximum average of K elements", "all subarrays of size K"

### When to Use Flexible Window:
- Find "smallest" or "longest" subarray
- Condition involves sum, count, distinct elements
- "At most K", "at least K", "exactly K"
- Examples: "smallest subarray with sum >= S"

### The "At Most" Trick:
```python
exactly_K = at_most_K - at_most_(K-1)
```
This works for:
- Exactly K distinct characters
- Exactly K odd numbers
- Exactly K of anything countable

### Optimization Pattern:
```
Brute Force (checking every subarray): O(N²) or O(N³)
                    ↓
    Sliding Window: O(N) or O(N*M) where M is small
```

---

## 🎓 FINAL TIPS

1. **Draw the window**: Visualize left and right pointers
2. **Track what changes**: When window moves, what updates?
3. **Edge cases**: Empty array, K=0, K=N, K>N
4. **State management**: Use hashmap for frequencies
5. **Practice pattern recognition**: After 20 problems, patterns become obvious

---

## ✅ STAIRCASE COMPLETION

Each stair builds on previous:
- **Stairs 1-2**: Basic window concepts → You understand what sliding means
- **Stairs 3-4**: Operations on windows → You can compute properties
- **Stair 5**: Flexible expansion → You can find optimal windows
- **Stair 6**: String techniques → You master complex problems

**Complete all stairs → Solve any sliding window problem with confidence! 🚀**

---

**Start with Staircase 1, Step 1.1 today! Draw the windows on paper and code each solution yourself.**

**Master this guide = Master Sliding Windows = Ace interviews! 💪**
