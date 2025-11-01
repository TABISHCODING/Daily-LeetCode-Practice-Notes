# 🎯 Two Pointer Mastery Guide - Master Every Trick & Manipulation

## 📘 Philosophy: Learn by Doing Micro-Steps

This guide teaches you **HOW TO THINK** with pointers through 100+ micro-questions.
Each pattern broken into tiny concepts with immediate practice.

**Learning Method**: Like learning to ride a bike - start with training wheels, gradually remove support.

---

## 🧠 Core Pointer Manipulation Concepts

### **The 5 Fundamental Pointer Operations:**

1. **INCREMENT**: `left++` or `right++` - Move forward
2. **DECREMENT**: `left--` or `right--` - Move backward  
3. **CONDITIONAL MOVE**: Move only if condition met
4. **SWAP**: Exchange values at two positions
5. **SKIP**: Jump over elements based on condition

---

## 📊 Pattern Deep Dive with Micro-Questions

---

## 🔵 PATTERN 1: OPPOSITE DIRECTION (LEFT-RIGHT)
**Core Concept**: Two pointers start at opposite ends, move towards each other

### **Essential Pointer Tricks:**

```python
# Trick 1: Basic Setup
left = 0
right = len(arr) - 1

# Trick 2: Stop Condition
while left < right:  # Stop when pointers meet/cross

# Trick 3: Comparison Logic
if arr[left] + arr[right] == target:
    # Found answer
elif arr[left] + arr[right] < target:
    left += 1  # Need larger value
else:
    right -= 1  # Need smaller value

# Trick 4: Boundary Check
if left >= right:  # Pointers crossed
    break
```

### **Common Conditions & Movements:**

| Condition | Action | Why |
|-----------|--------|-----|
| `sum < target` | `left++` | Increase sum (in sorted array) |
| `sum > target` | `right--` | Decrease sum |
| `arr[left] == arr[right]` | `left++, right--` | Match found, check next |
| `arr[left] != arr[right]` | `return False` | Not palindrome |
| `left == right` | `return arr[left]` | Single element left |

---

### 🎓 MICRO-LEVEL EXERCISES - OPPOSITE DIRECTION

#### **Stage 1: Understanding Index Movement (5 Questions)**

**Q1.1: Print Pointer Positions**
```
Problem: Print left and right pointer values at each step
Input: [1, 2, 3, 4, 5]
Output: 
  Step 1: left=0 (val=1), right=4 (val=5)
  Step 2: left=1 (val=2), right=3 (val=4)
  Step 3: left=2 (val=3), right=2 (val=3)

Solution:
def print_positions(arr):
    left, right = 0, len(arr) - 1
    step = 1
    while left <= right:
        print(f"Step {step}: left={left} (val={arr[left]}), right={right} (val={arr[right]})")
        left += 1
        right -= 1
        step += 1
```

**Q1.2: Count Steps Until Pointers Meet**
```
Problem: How many steps before left >= right?
Input: [1, 2, 3, 4, 5, 6]
Output: 3

Hint: Each iteration moves both pointers
Solution:
def count_steps(arr):
    left, right = 0, len(arr) - 1
    steps = 0
    while left < right:
        steps += 1
        left += 1
        right -= 1
    return steps
```

**Q1.3: What Index After N Moves?**
```
Problem: Where will left be after 3 moves? Where will right be?
Input: arr = [10, 20, 30, 40, 50, 60, 70], moves = 3
Output: left at index 3, right at index 3

Solution:
def position_after_moves(arr, moves):
    left, right = 0, len(arr) - 1
    for _ in range(moves):
        if left < right:
            left += 1
            right -= 1
    return left, right
```

**Q1.4: Middle Element Finding**
```
Problem: When pointers meet, print the middle element(s)
Input: [1, 2, 3, 4, 5]
Output: 3 (single middle)

Input: [1, 2, 3, 4]
Output: 2, 3 (two middle elements)

Solution:
def find_middle(arr):
    left, right = 0, len(arr) - 1
    while left < right:
        left += 1
        right -= 1
    if left == right:
        return [arr[left]]
    else:
        return [arr[right], arr[left]]  # right is now left-1
```

**Q1.5: Selective Movement**
```
Problem: Move left only, keep right fixed. Print positions.
Input: [1, 2, 3, 4, 5]
Output:
  (0, 4), (1, 4), (2, 4), (3, 4), (4, 4)

Solution:
def move_left_only(arr):
    left, right = 0, len(arr) - 1
    positions = []
    while left <= right:
        positions.append((left, right))
        left += 1
    return positions
```

---

#### **Stage 2: Basic Comparisons (10 Questions)**

**Q2.1: Check if First Equals Last**
```
Problem: Compare first and last element
Input: [5, 2, 3, 5]
Output: True

Input: [1, 2, 3, 4]
Output: False

Solution:
def first_equals_last(arr):
    left, right = 0, len(arr) - 1
    return arr[left] == arr[right]
```

**Q2.2: Check All Opposite Pairs Are Equal**
```
Problem: Check if arr[0]==arr[n-1], arr[1]==arr[n-2], etc.
Input: [1, 2, 2, 1]
Output: True

Input: [1, 2, 3, 4]
Output: False

Solution:
def all_pairs_equal(arr):
    left, right = 0, len(arr) - 1
    while left < right:
        if arr[left] != arr[right]:
            return False
        left += 1
        right -= 1
    return True
```

**Q2.3: Count Equal Pairs**
```
Problem: Count how many opposite pairs are equal
Input: [1, 2, 3, 2, 1]
Output: 2 (pairs: 1==1, 2==2)

Solution:
def count_equal_pairs(arr):
    left, right = 0, len(arr) - 1
    count = 0
    while left < right:
        if arr[left] == arr[right]:
            count += 1
        left += 1
        right -= 1
    return count
```

**Q2.4: Find First Unequal Pair**
```
Problem: Return indices where arr[left] != arr[right] first
Input: [1, 2, 3, 2, 5]
Output: (0, 4) because arr[0]=1, arr[4]=5

Solution:
def first_unequal_pair(arr):
    left, right = 0, len(arr) - 1
    while left < right:
        if arr[left] != arr[right]:
            return (left, right)
        left += 1
        right -= 1
    return None
```

**Q2.5: Check Palindrome (Numbers)**
```
Problem: Is array palindrome?
Input: [1, 2, 3, 2, 1]
Output: True

Solution:
def is_palindrome_array(arr):
    left, right = 0, len(arr) - 1
    while left < right:
        if arr[left] != arr[right]:
            return False
        left += 1
        right -= 1
    return True
```

**Q2.6: Check Palindrome (Strings - Basic)**
```
Problem: Is string palindrome? (case-sensitive)
Input: "racecar"
Output: True

Input: "hello"
Output: False

Solution:
def is_palindrome_string(s):
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True
```

**Q2.7: Check Palindrome (Ignore Case)**
```
Problem: Case-insensitive palindrome
Input: "RaceCar"
Output: True

Solution:
def is_palindrome_ignore_case(s):
    left, right = 0, len(s) - 1
    while left < right:
        if s[left].lower() != s[right].lower():
            return False
        left += 1
        right -= 1
    return True
```

**Q2.8: Compare Sum of Halves**
```
Problem: Sum of first half vs second half
Input: [1, 2, 3, 4]
Output: Equal (1+2 = 3+4)

Solution:
def compare_halves(arr):
    left, right = 0, len(arr) - 1
    left_sum, right_sum = 0, 0
    while left < right:
        left_sum += arr[left]
        right_sum += arr[right]
        left += 1
        right -= 1
    return "Equal" if left_sum == right_sum else "Not Equal"
```

**Q2.9: Find Maximum Opposite Pair Sum**
```
Problem: Maximum of (arr[0]+arr[n-1], arr[1]+arr[n-2], ...)
Input: [1, 2, 3, 4, 5]
Output: 6 (from 1+5 or 2+4)

Solution:
def max_opposite_sum(arr):
    left, right = 0, len(arr) - 1
    max_sum = float('-inf')
    while left < right:
        max_sum = max(max_sum, arr[left] + arr[right])
        left += 1
        right -= 1
    return max_sum
```

**Q2.10: Find Minimum Opposite Pair Sum**
```
Problem: Minimum opposite pair sum
Input: [5, 3, 8, 1, 9]
Output: 6 (from 5+1)

Solution:
def min_opposite_sum(arr):
    left, right = 0, len(arr) - 1
    min_sum = float('inf')
    while left < right:
        min_sum = min(min_sum, arr[left] + arr[right])
        left += 1
        right -= 1
    return min_sum
```

---

#### **Stage 3: Swapping & Reversing (10 Questions)**

**Q3.1: Swap First and Last**
```
Problem: Swap only first and last element
Input: [1, 2, 3, 4, 5]
Output: [5, 2, 3, 4, 1]

Solution:
def swap_first_last(arr):
    left, right = 0, len(arr) - 1
    arr[left], arr[right] = arr[right], arr[left]
    return arr
```

**Q3.2: Swap All Opposite Pairs**
```
Problem: Swap arr[0]↔arr[n-1], arr[1]↔arr[n-2], etc.
Input: [1, 2, 3, 4]
Output: [4, 3, 2, 1]

Solution:
def swap_all_pairs(arr):
    left, right = 0, len(arr) - 1
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
    return arr
```

**Q3.3: Reverse Array In-Place**
```
Problem: Reverse array using two pointers
Input: [1, 2, 3, 4, 5]
Output: [5, 4, 3, 2, 1]

Solution:
def reverse_array(arr):
    left, right = 0, len(arr) - 1
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
    return arr
```

**Q3.4: Reverse String**
```
Problem: Reverse string (convert to list first)
Input: "hello"
Output: "olleh"

Solution:
def reverse_string(s):
    arr = list(s)
    left, right = 0, len(arr) - 1
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
    return ''.join(arr)
```

**Q3.5: Reverse Only First Half**
```
Problem: Reverse only elements from 0 to mid
Input: [1, 2, 3, 4, 5]
Output: [2, 1, 3, 4, 5]

Solution:
def reverse_first_half(arr):
    mid = len(arr) // 2
    left, right = 0, mid - 1
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
    return arr
```

**Q3.6: Reverse Only Second Half**
```
Problem: Reverse elements from mid to end
Input: [1, 2, 3, 4, 5]
Output: [1, 2, 3, 5, 4]

Solution:
def reverse_second_half(arr):
    mid = len(arr) // 2
    left, right = mid, len(arr) - 1
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
    return arr
```

**Q3.7: Conditional Swap (Only if Left < Right)**
```
Problem: Swap only if arr[left] < arr[right]
Input: [5, 2, 8, 1, 9]
Output: [9, 2, 8, 1, 5] (swapped 5↔9)

Solution:
def conditional_swap(arr):
    left, right = 0, len(arr) - 1
    while left < right:
        if arr[left] < arr[right]:
            arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
    return arr
```

**Q3.8: Swap Count**
```
Problem: Count how many swaps performed in reverse
Input: [1, 2, 3, 4, 5]
Output: 2 (swaps: 1↔5, 2↔4)

Solution:
def count_swaps(arr):
    left, right = 0, len(arr) - 1
    swaps = 0
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        swaps += 1
        left += 1
        right -= 1
    return swaps
```

**Q3.9: Reverse Words in String**
```
Problem: Reverse each word (not entire string)
Input: "hello world"
Output: "olleh dlrow"

Solution:
def reverse_words(s):
    words = s.split()
    result = []
    for word in words:
        left, right = 0, len(word) - 1
        word_list = list(word)
        while left < right:
            word_list[left], word_list[right] = word_list[right], word_list[left]
            left += 1
            right -= 1
        result.append(''.join(word_list))
    return ' '.join(result)
```

**Q3.10: Reverse Only Vowels**
```
Problem: Reverse only vowel positions
Input: "hello"
Output: "holle"

Solution:
def reverse_vowels(s):
    vowels = set('aeiouAEIOU')
    arr = list(s)
    left, right = 0, len(arr) - 1
    
    while left < right:
        # Move left until vowel found
        while left < right and arr[left] not in vowels:
            left += 1
        # Move right until vowel found
        while left < right and arr[right] not in vowels:
            right -= 1
        
        # Swap vowels
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
    
    return ''.join(arr)
```

---

#### **Stage 4: Conditional Movements (15 Questions)**

**Q4.1: Skip Zeros from Left**
```
Problem: Move left pointer past all zeros
Input: [0, 0, 1, 2, 3]
Output: left stops at index 2

Solution:
def skip_left_zeros(arr):
    left = 0
    while left < len(arr) and arr[left] == 0:
        left += 1
    return left
```

**Q4.2: Skip Zeros from Right**
```
Problem: Move right pointer past all zeros from end
Input: [1, 2, 3, 0, 0]
Output: right stops at index 2

Solution:
def skip_right_zeros(arr):
    right = len(arr) - 1
    while right >= 0 and arr[right] == 0:
        right -= 1
    return right
```

**Q4.3: Skip Both Ends**
```
Problem: Skip zeros from both ends
Input: [0, 0, 1, 2, 0, 0]
Output: left=2, right=3

Solution:
def skip_both_ends(arr):
    left, right = 0, len(arr) - 1
    
    while left < len(arr) and arr[left] == 0:
        left += 1
    
    while right >= 0 and arr[right] == 0:
        right -= 1
    
    return left, right
```

**Q4.4: Move Left Until Condition**
```
Problem: Move left until arr[left] > 5
Input: [1, 2, 3, 6, 7]
Output: left=3

Solution:
def move_until_condition(arr):
    left = 0
    while left < len(arr) and arr[left] <= 5:
        left += 1
    return left
```

**Q4.5: Two Sum in Sorted Array**
```
Problem: Find two numbers that sum to target
Input: arr = [1, 2, 3, 4, 6], target = 6
Output: [1, 3] (indices) → values 2+4=6

Solution:
def two_sum_sorted(arr, target):
    left, right = 0, len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1  # Need larger sum
        else:
            right -= 1  # Need smaller sum
    
    return []
```

**Q4.6: Two Sum - Find All Pairs**
```
Problem: Find ALL pairs that sum to target
Input: arr = [1, 2, 3, 4, 5, 6], target = 7
Output: [(1,6), (2,5), (3,4)]

Solution:
def two_sum_all_pairs(arr, target):
    left, right = 0, len(arr) - 1
    pairs = []
    
    while left < right:
        current_sum = arr[left] + arr[right]
        
        if current_sum == target:
            pairs.append((arr[left], arr[right]))
            left += 1
            right -= 1
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return pairs
```

**Q4.7: Two Sum - Count Pairs**
```
Problem: Count pairs with sum equal to target
Input: arr = [1, 2, 3, 4, 5, 6], target = 7
Output: 3

Solution:
def count_pairs_sum(arr, target):
    left, right = 0, len(arr) - 1
    count = 0
    
    while left < right:
        current_sum = arr[left] + arr[right]
        
        if current_sum == target:
            count += 1
            left += 1
            right -= 1
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return count
```

**Q4.8: Find Pair with Difference K**
```
Problem: Find pair where arr[right] - arr[left] = K
Input: arr = [1, 3, 5, 7, 9], K = 4
Output: (1, 5) or (5, 9)

Solution:
def pair_with_difference(arr, K):
    left, right = 0, 1
    
    while right < len(arr):
        diff = arr[right] - arr[left]
        
        if diff == K:
            return (arr[left], arr[right])
        elif diff < K:
            right += 1  # Need larger difference
        else:
            left += 1  # Need smaller difference
            if left == right:  # Keep them apart
                right += 1
    
    return None
```

**Q4.9: Closest Sum to Target**
```
Problem: Find pair with sum closest to target
Input: arr = [1, 2, 3, 4, 6], target = 10
Output: (4, 6) → sum=10

Solution:
def closest_sum(arr, target):
    left, right = 0, len(arr) - 1
    closest = float('inf')
    result = []
    
    while left < right:
        current_sum = arr[left] + arr[right]
        
        if abs(target - current_sum) < abs(target - closest):
            closest = current_sum
            result = [arr[left], arr[right]]
        
        if current_sum < target:
            left += 1
        else:
            right -= 1
    
    return result
```

**Q4.10: Count Pairs with Sum Less Than Target**
```
Problem: Count all pairs where sum < target
Input: arr = [1, 2, 3, 4], target = 6
Output: 4 pairs: (1,2), (1,3), (1,4), (2,3)

Solution:
def count_pairs_less_than(arr, target):
    left, right = 0, len(arr) - 1
    count = 0
    
    while left < right:
        if arr[left] + arr[right] < target:
            # All pairs (left, left+1...right) are valid
            count += right - left
            left += 1
        else:
            right -= 1
    
    return count
```

**Q4.11: Container With Most Water (Simplified)**
```
Problem: Find max area between two lines
Input: heights = [1, 8, 6, 2, 5, 4, 8, 3, 7]
Output: 49

Solution:
def max_water(heights):
    left, right = 0, len(heights) - 1
    max_area = 0
    
    while left < right:
        # Area = min height * width
        height = min(heights[left], heights[right])
        width = right - left
        area = height * width
        max_area = max(max_area, area)
        
        # Move pointer with smaller height
        if heights[left] < heights[right]:
            left += 1
        else:
            right -= 1
    
    return max_area
```

**Q4.12: Move Left Only When Sum Exceeds**
```
Problem: Keep moving right, move left when sum > target
Input: arr = [1, 2, 3, 4, 5], target = 8
Track movement

Solution:
def conditional_left_move(arr, target):
    left = 0
    movements = []
    
    for right in range(len(arr)):
        while left < right and arr[left] + arr[right] > target:
            movements.append(f"Sum {arr[left]}+{arr[right]}>{target}, move left")
            left += 1
        movements.append(f"Left={left}, Right={right}")
    
    return movements
```

**Q4.13: Skip Duplicates from Both Ends**
```
Problem: Skip duplicate values from both ends
Input: [1, 1, 2, 3, 4, 4, 4]
Output: left=2, right=4

Solution:
def skip_duplicates(arr):
    if not arr:
        return -1, -1
    
    left, right = 0, len(arr) - 1
    
    # Skip duplicates from left
    while left < len(arr) - 1 and arr[left] == arr[left + 1]:
        left += 1
    
    # Skip duplicates from right
    while right > 0 and arr[right] == arr[right - 1]:
        right -= 1
    
    return left, right
```

**Q4.14: Valid Palindrome (Skip Non-Alphanumeric)**
```
Problem: Check palindrome ignoring special characters
Input: "A man, a plan, a canal: Panama"
Output: True

Solution:
def is_valid_palindrome(s):
    left, right = 0, len(s) - 1
    
    while left < right:
        # Skip non-alphanumeric from left
        while left < right and not s[left].isalnum():
            left += 1
        
        # Skip non-alphanumeric from right
        while left < right and not s[right].isalnum():
            right -= 1
        
        # Compare
        if s[left].lower() != s[right].lower():
            return False
        
        left += 1
        right -= 1
    
    return True
```

**Q4.15: Sort Array with 0s and 1s**
```
Problem: Move all 0s to left, 1s to right
Input: [1, 0, 1, 0, 1, 0]
Output: [0, 0, 0, 1, 1, 1]

Solution:
def sort_binary(arr):
    left, right = 0, len(arr) - 1
    
    while left < right:
        # Move left past all 0s
        while left < right and arr[left] == 0:
            left += 1
        
        # Move right past all 1s
        while left < right and arr[right] == 1:
            right -= 1
        
        # Swap misplaced elements
        if left < right:
            arr[left], arr[right] = arr[right], arr[left]
            left += 1
            right -= 1
    
    return arr
```

---

## 🟢 PATTERN 2: SAME DIRECTION (SLOW-FAST)
**Core Concept**: Both pointers move forward, one faster than other

### **Essential Pointer Tricks:**

```python
# Trick 1: Basic Setup
slow = 0
fast = 0  # or fast = 1 depending on problem

# Trick 2: Fast Explores, Slow Builds Result
for fast in range(len(arr)):
    if condition:
        arr[slow] = arr[fast]
        slow += 1

# Trick 3: Slow Tracks "Good" Position
# Fast finds "good" elements
# Slow marks where to place them

# Trick 4: Fast Multiple Steps
while fast < len(arr):
    # Fast can move multiple steps
    fast += 2  # Or based on condition
```

### **Common Patterns:**

| Use Case | Slow Purpose | Fast Purpose |
|----------|--------------|--------------|
| Remove duplicates | Last unique position | Find next unique |
| Move zeros | Position for non-zero | Find non-zeros |
| Remove element | Build new array | Explore all elements |
| Partition | Boundary of partition | Scan elements |

---

### 🎓 MICRO-LEVEL EXERCISES - SAME DIRECTION

#### **Stage 5: Basic Slow-Fast Movement (10 Questions)**

**Q5.1: Visualize Slow-Fast Movement**
```
Problem: Print slow and fast at each step (fast moves every iteration)
Input: [1, 2, 3, 4, 5]
Output:
  Step 1: slow=0, fast=0
  Step 2: slow=0, fast=1
  Step 3: slow=0, fast=2
  ...

Solution:
def visualize_slow_fast(arr):
    slow = 0
    for fast in range(len(arr)):
        print(f"Step {fast+1}: slow={slow}, fast={fast}")
```

**Q5.2: Move Slow Only When Condition Met**
```
Problem: Move slow only when arr[fast] is even
Input: [1, 2, 3, 4, 5, 6]
Output: slow moves 3 times (for 2, 4, 6)

Solution:
def conditional_slow_move(arr):
    slow = 0
    moves = 0
    
    for fast in range(len(arr)):
        if arr[fast] % 2 == 0:
            slow += 1
            moves += 1
    
    return moves
```

**Q5.3: Copy Even Numbers**
```
Problem: Copy all even numbers to front of array
Input: [1, 2, 3, 4, 5, 6]
Output: [2, 4, 6, 4, 5, 6] (first 3 are even)

Solution:
def copy_evens(arr):
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] % 2 == 0:
            arr[slow] = arr[fast]
            slow += 1
    
    return arr
```

**Q5.4: Count Non-Zero Elements**
```
Problem: Count non-zero elements using slow-fast
Input: [1, 0, 2, 0, 3]
Output: 3

Solution:
def count_non_zero(arr):
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] != 0:
            slow += 1
    
    return slow
```

**Q5.5: Remove Duplicates from Sorted Array (Basic)**
```
Problem: Remove duplicates, return new length
Input: [1, 1, 2, 2, 3]
Output: 3, array becomes [1, 2, 3, _, _]

Solution:
def remove_duplicates(arr):
    if not arr:
        return 0
    
    slow = 0  # Last unique position
    
    for fast in range(1, len(arr)):
        if arr[fast] != arr[slow]:
            slow += 1
            arr[slow] = arr[fast]
    
    return slow + 1
```

**Q5.6: Count Unique Elements**
```
Problem: Just count, don't modify array
Input: [1, 1, 2, 2, 3, 3, 3]
Output: 3

Solution:
def count_unique(arr):
    if not arr:
        return 0
    
    count = 1  # First element is always unique
    
    for i in range(1, len(arr)):
        if arr[i] != arr[i-1]:
            count += 1
    
    return count
```

**Q5.7: Remove Specific Element**
```
Problem: Remove all occurrences of val
Input: arr = [3, 2, 2, 3], val = 3
Output: 2, array becomes [2, 2, _, _]

Solution:
def remove_element(arr, val):
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] != val:
            arr[slow] = arr[fast]
            slow += 1
    
    return slow
```

**Q5.8: Keep Only Positive Numbers**
```
Problem: Move all positive numbers to front
Input: [-1, 2, -3, 4, -5, 6]
Output: [2, 4, 6, _, _, _], return 3

Solution:
def keep_positives(arr):
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] > 0:
            arr[slow] = arr[fast]
            slow += 1
    
    return slow
```

**Q5.9: Remove All Zeros**
```
Problem: Remove zeros, shift others left
Input: [0, 1, 0, 2, 0, 3]
Output: [1, 2, 3, _, _, _], return 3

Solution:
def remove_zeros(arr):
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] != 0:
            arr[slow] = arr[fast]
            slow += 1
    
    return slow
```

**Q5.10: Separate by Condition**
```
Problem: Move numbers < 5 to front
Input: [3, 7, 2, 8, 1, 9, 4]
Output: [3, 2, 1, 4, _, _, _], return 4

Solution:
def separate_by_condition(arr, threshold=5):
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] < threshold:
            arr[slow] = arr[fast]
            slow += 1
    
    return slow
```

---

#### **Stage 6: Move Zeros Pattern (10 Questions)**

**Q5.11: Move Zeros to End (Standard)**
```
Problem: Move all zeros to end, maintain order
Input: [0, 1, 0, 3, 12]
Output: [1, 3, 12, 0, 0]

Solution:
def move_zeros(arr):
    slow = 0  # Position for next non-zero
    
    # Move all non-zeros to front
    for fast in range(len(arr)):
        if arr[fast] != 0:
            arr[slow] = arr[fast]
            slow += 1
    
    # Fill remaining with zeros
    for i in range(slow, len(arr)):
        arr[i] = 0
    
    return arr
```

**Q5.12: Move Zeros with Swap**
```
Problem: Same as above but using swap
Input: [0, 1, 0, 3, 12]
Output: [1, 3, 12, 0, 0]

Solution:
def move_zeros_swap(arr):
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] != 0:
            # Swap non-zero with slow position
            arr[slow], arr[fast] = arr[fast], arr[slow]
            slow += 1
    
    return arr
```

**Q5.13: Count Zeros Moved**
```
Problem: How many zeros were moved?
Input: [0, 1, 0, 3, 12]
Output: 2

Solution:
def count_zeros_moved(arr):
    zero_count = 0
    
    for num in arr:
        if num == 0:
            zero_count += 1
    
    return zero_count
```

**Q5.14: Move Negative Numbers to End**
```
Problem: Move negative numbers to end
Input: [1, -2, 3, -4, 5]
Output: [1, 3, 5, -2, -4]

Solution:
def move_negatives(arr):
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] >= 0:
            arr[slow] = arr[fast]
            slow += 1
    
    # Fill remaining with negatives
    for fast in range(len(arr)):
        if arr[fast] < 0:
            arr[slow] = arr[fast]
            slow += 1
    
    return arr
```

**Q5.15: Move Even Numbers to Front**
```
Problem: Move evens to front, odds to back
Input: [1, 2, 3, 4, 5, 6]
Output: [2, 4, 6, 1, 3, 5]

Solution:
def move_evens_front(arr):
    slow = 0
    
    # Move evens to front
    for fast in range(len(arr)):
        if arr[fast] % 2 == 0:
            arr[slow] = arr[fast]
            slow += 1
    
    # Move odds to back
    for fast in range(len(arr)):
        if arr[fast] % 2 != 0:
            arr[slow] = arr[fast]
            slow += 1
    
    return arr
```

**Q5.16: Move Zeros, Track Swaps**
```
Problem: Count how many swaps made
Input: [0, 1, 0, 3, 12]
Output: 3 swaps

Solution:
def move_zeros_count_swaps(arr):
    slow = 0
    swaps = 0
    
    for fast in range(len(arr)):
        if arr[fast] != 0:
            if slow != fast:
                arr[slow], arr[fast] = arr[fast], arr[slow]
                swaps += 1
            slow += 1
    
    return swaps
```

**Q5.17: Move Duplicates to End**
```
Problem: Move duplicate elements to end
Input: [1, 2, 2, 3, 3, 4]
Output: [1, 2, 3, 4, 2, 3]

Solution:
def move_duplicates(arr):
    if not arr:
        return arr
    
    slow = 1  # Start from second element
    
    for fast in range(1, len(arr)):
        if arr[fast] != arr[fast-1]:
            arr[slow] = arr[fast]
            slow += 1
    
    # Fill rest with duplicates
    # (simplified - in practice would need to track them)
    
    return arr
```

**Q5.18: Partition Array by Value**
```
Problem: Move elements < pivot to left
Input: arr = [3, 5, 1, 4, 2], pivot = 3
Output: [1, 2, 3, 5, 4] (< 3 on left)

Solution:
def partition_by_value(arr, pivot):
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] < pivot:
            arr[slow], arr[fast] = arr[fast], arr[slow]
            slow += 1
    
    return arr
```

**Q5.19: Remove Consonants from String**
```
Problem: Keep only vowels
Input: "hello"
Output: "eo"

Solution:
def keep_vowels(s):
    vowels = set('aeiouAEIOU')
    arr = list(s)
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] in vowels:
            arr[slow] = arr[fast]
            slow += 1
    
    return ''.join(arr[:slow])
```

**Q5.20: Move Characters to End**
```
Problem: Move all 'x' to end
Input: "xaxxbxc"
Output: "abcxxxx"

Solution:
def move_char_to_end(s, char='x'):
    arr = list(s)
    slow = 0
    
    for fast in range(len(arr)):
        if arr[fast] != char:
            arr[slow] = arr[fast]
            slow += 1
    
    # Fill rest with char
    for i in range(slow, len(arr)):
        arr[i] = char
    
    return ''.join(arr)
```

---

#### **Stage 7: Advanced Slow-Fast (5 Questions)**

**Q5.21: Remove Duplicates - Keep Two**
```
Problem: Allow up to 2 duplicates
Input: [1, 1, 1, 2, 2, 3]
Output: [1, 1, 2, 2, 3, _], return 5

Solution:
def remove_duplicates_keep_two(arr):
    if len(arr) <= 2:
        return len(arr)
    
    slow = 2  # First two elements stay
    
    for fast in range(2, len(arr)):
        # Keep if different from element 2 positions back
        if arr[fast] != arr[slow - 2]:
            arr[slow] = arr[fast]
            slow += 1
    
    return slow
```

**Q5.22: Squares of Sorted Array (Negative Numbers)**
```
Problem: Square array and return sorted
Input: [-4, -1, 0, 3, 10]
Output: [0, 1, 9, 16, 100]

Solution:
def sorted_squares(arr):
    n = len(arr)
    result = [0] * n
    left, right = 0, n - 1
    pos = n - 1  # Fill from end
    
    while left <= right:
        left_sq = arr[left] ** 2
        right_sq = arr[right] ** 2
        
        if left_sq > right_sq:
            result[pos] = left_sq
            left += 1
        else:
            result[pos] = right_sq
            right -= 1
        
        pos -= 1
    
    return result
```

**Q5.23: Dutch National Flag (3-Way Partition)**
```
Problem: Sort 0s, 1s, 2s in-place
Input: [2, 0, 2, 1, 1, 0]
Output: [0, 0, 1, 1, 2, 2]

Solution:
def sort_colors(arr):
    low = 0      # Boundary for 0s
    mid = 0      # Current element
    high = len(arr) - 1  # Boundary for 2s
    
    while mid <= high:
        if arr[mid] == 0:
            arr[low], arr[mid] = arr[mid], arr[low]
            low += 1
            mid += 1
        elif arr[mid] == 1:
            mid += 1
        else:  # arr[mid] == 2
            arr[mid], arr[high] = arr[high], arr[mid]
            high -= 1
    
    return arr
```

**Q5.24: Partition Labels**
```
Problem: Find minimum segments where each letter appears in only one segment
Input: "ababcbacadefegdehijhklij"
Output: [9, 7, 8]

Solution:
def partition_labels(s):
    # Find last occurrence of each character
    last = {c: i for i, c in enumerate(s)}
    
    result = []
    start = 0
    end = 0
    
    for i, c in enumerate(s):
        end = max(end, last[c])
        
        if i == end:
            result.append(end - start + 1)
            start = i + 1
    
    return result
```

**Q5.25: Backspace String Compare** ⭐
```
Problem: Compare two strings with backspace (#)
Input: s = "ab#c", t = "ad#c"
Output: True (both become "ac")

Solution - Using Two Pointers from End:
def backspace_compare(s, t):
    def next_valid_char(string, index):
        backspace = 0
        while index >= 0:
            if string[index] == '#':
                backspace += 1
            elif backspace > 0:
                backspace -= 1
            else:
                break
            index -= 1
        return index
    
    i, j = len(s) - 1, len(t) - 1
    
    while i >= 0 or j >= 0:
        i = next_valid_char(s, i)
        j = next_valid_char(t, j)
        
        # Both reached end
        if i < 0 and j < 0:
            return True
        
        # One reached end
        if i < 0 or j < 0:
            return False
        
        # Characters don't match
        if s[i] != t[j]:
            return False
        
        i -= 1
        j -= 1
    
    return True

# Why from end? Backspace affects previous characters, easier to process backwards
```

---

## 🟡 PATTERN 3: SLIDING WINDOW - FIXED SIZE

### **Essential Pointer Tricks:**

```python
# Trick 1: Fixed Window Setup
window_size = k
left = 0
right = k - 1

# Trick 2: Calculate First Window
window_sum = sum(arr[0:k])

# Trick 3: Slide Window
for i in range(k, len(arr)):
    window_sum = window_sum - arr[i-k] + arr[i]
    # OR
    window_sum -= arr[left]
    left += 1
    right += 1
    window_sum += arr[right]

# Trick 4: Window Size Formula
window_size = right - left + 1
```

### **Common Operations:**

| Operation | Code | Purpose |
|-----------|------|---------|
| Initialize window | `sum(arr[0:k])` | First window sum |
| Slide right | `sum += arr[right]; right++` | Add new element |
| Remove left | `sum -= arr[left]; left++` | Remove old element |
| Check size | `right - left + 1 == k` | Verify window size |

---

### 🎓 MICRO-LEVEL EXERCISES - FIXED WINDOW

#### **Stage 8: Basic Fixed Window (10 Questions)**

**Q6.1: Print All Windows of Size K**
```
Problem: Print all subarrays of size K
Input: arr = [1, 2, 3, 4, 5], K = 3
Output: [1,2,3], [2,3,4], [3,4,5]

Solution:
def print_windows(arr, k):
    windows = []
    
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        windows.append(window)
        print(window)
    
    return windows
```

**Q6.2: Count Windows**
```
Problem: How many windows of size K exist?
Input: arr = [1, 2, 3, 4, 5], K = 3
Output: 3

Solution:
def count_windows(arr, k):
    if len(arr) < k:
        return 0
    return len(arr) - k + 1
```

**Q6.3: Sum of First Window**
```
Problem: Calculate sum of first K elements
Input: arr = [1, 2, 3, 4, 5], K = 3
Output: 6

Solution:
def first_window_sum(arr, k):
    return sum(arr[:k])
```

**Q6.4: All Window Sums (Brute Force)**
```
Problem: Calculate sum of each window
Input: arr = [1, 2, 3, 4, 5], K = 3
Output: [6, 9, 12]

Solution:
def all_window_sums_brute(arr, k):
    sums = []
    
    for i in range(len(arr) - k + 1):
        window_sum = sum(arr[i:i+k])
        sums.append(window_sum)
    
    return sums
```

**Q6.5: All Window Sums (Optimized - Sliding)**
```
Problem: Same as above, but optimize using sliding
Input: arr = [1, 2, 3, 4, 5], K = 3
Output: [6, 9, 12]

Solution:
def all_window_sums_optimized(arr, k):
    if len(arr) < k:
        return []
    
    sums = []
    window_sum = sum(arr[:k])
    sums.append(window_sum)
    
    # Slide window
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        sums.append(window_sum)
    
    return sums
```

**Q6.6: Maximum Window Sum**
```
Problem: Find maximum sum of any K consecutive elements
Input: arr = [2, 1, 5, 1, 3, 2], K = 3
Output: 9 (from [5, 1, 3])

Solution:
def max_window_sum(arr, k):
    if len(arr) < k:
        return 0
    
    # First window
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    # Slide and compare
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum
```

**Q6.7: Minimum Window Sum**
```
Problem: Find minimum sum of K consecutive elements
Input: arr = [2, 1, 5, 1, 3, 2], K = 3
Output: 4 (from [2, 1, 1] - wait, that's not K consecutive...)
Actually: [1, 3, 2] = 6 or [2, 1, 5] = 8, min is 6

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

**Q6.8: Average of All K-Size Windows**
```
Problem: Calculate average of each window
Input: arr = [1, 3, 2, 6, -1, 4, 1, 8, 2], K = 5
Output: [2.2, 2.8, 2.4, 3.6, 2.8]

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

**Q6.9: Count Windows with Sum > Target**
```
Problem: Count windows where sum exceeds target
Input: arr = [2, 1, 5, 1, 3, 2], K = 3, target = 7
Output: 1 (only [5, 1, 3])

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

**Q6.10: Find Maximum in Each Window**
```
Problem: Find maximum element in each K-size window
Input: arr = [1, 3, -1, -3, 5, 3, 6, 7], K = 3
Output: [3, 3, 5, 5, 6, 7]

Solution:
def max_in_each_window(arr, k):
    if len(arr) < k:
        return []
    
    result = []
    
    for i in range(len(arr) - k + 1):
        window_max = max(arr[i:i+k])
        result.append(window_max)
    
    return result
```

---

#### **Stage 9: Product & Other Operations (5 Questions)**

**Q6.11: Maximum Product of K Elements**
```
Problem: Find maximum product of K consecutive elements
Input: arr = [2, 3, -2, 4], K = 2
Output: 6 (from [2, 3])

Solution:
def max_product_window(arr, k):
    if len(arr) < k:
        return 0
    
    # Calculate first window product
    window_product = 1
    for i in range(k):
        window_product *= arr[i]
    
    max_product = window_product
    
    # Slide window
    for i in range(k, len(arr)):
        # Divide by element leaving, multiply by element entering
        window_product = (window_product // arr[i-k]) * arr[i]
        max_product = max(max_product, window_product)
    
    return max_product
```

**Q6.12: Count Distinct Elements in Each Window**
```
Problem: Count unique elements in each K-size window
Input: arr = [1, 2, 1, 3, 4, 2, 3], K = 4
Output: [3, 4, 4, 3]

Solution:
def distinct_in_windows(arr, k):
    result = []
    
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        distinct_count = len(set(window))
        result.append(distinct_count)
    
    return result
```

**Q6.13: First Negative in Each Window**
```
Problem: Find first negative number in each window
Input: arr = [12, -1, -7, 8, -15, 30, 16, 28], K = 3
Output: [-1, -1, -7, -15, -15, 0]

Solution:
def first_negative_in_windows(arr, k):
    result = []
    
    for i in range(len(arr) - k + 1):
        window = arr[i:i+k]
        first_neg = next((x for x in window if x < 0), 0)
        result.append(first_neg)
    
    return result
```

**Q6.14: Count Vowels in Each Window (String)**
```
Problem: Count vowels in each K-character window
Input: s = "abciiidef", K = 3
Output: [1, 1, 3, 3, 2, 1, 1]

Solution:
def vowels_in_windows(s, k):
    vowels = set('aeiouAEIOU')
    result = []
    
    for i in range(len(s) - k + 1):
        window = s[i:i+k]
        vowel_count = sum(1 for c in window if c in vowels)
        result.append(vowel_count)
    
    return result
```

**Q6.15: Maximum Sum Circular Subarray (Fixed K)**
```
Problem: Array is circular, find max sum of K elements
Input: arr = [1, 2, 3, 4, 5], K = 2
Output: 9 (from [5, 1] circular)

Solution:
def max_sum_circular(arr, k):
    n = len(arr)
    max_sum = float('-inf')
    
    # Extend array to handle circular nature
    extended = arr + arr
    
    window_sum = sum(extended[:k])
    max_sum = window_sum
    
    for i in range(k, n + k):
        window_sum = window_sum - extended[i-k] + extended[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum
```

---

## 🟠 PATTERN 4: FLEXIBLE WINDOW (VARIABLE SIZE)

### **Essential Pointer Tricks:**

```python
# Trick 1: Expand-Shrink Pattern
left = 0
for right in range(len(arr)):
    # Expand: Add arr[right] to window
    window_sum += arr[right]
    
    # Shrink: Remove from left while condition violated
    while condition_violated:
        window_sum -= arr[left]
        left += 1
    
    # Update result
    max_length = max(max_length, right - left + 1)

# Trick 2: Use HashMap for Frequency
window = {}  # or defaultdict(int)
window[arr[right]] = window.get(arr[right], 0) + 1

# Trick 3: Window Size Calculation
current_size = right - left + 1

# Trick 4: Valid Window Check
is_valid = len(window) <= k  # For k distinct elements
```

### **Common Patterns:**

| Problem Type | Expand When | Shrink When | Track |
|--------------|-------------|-------------|-------|
| Min subarray sum >= S | Always | sum >= S | min_length |
| Max subarray sum <= S | Always | sum > S | max_length |
| Longest K distinct | Always | distinct > K | max_length |
| Shortest K distinct | Always | distinct >= K | min_length |

---

### 🎓 MICRO-LEVEL EXERCISES - FLEXIBLE WINDOW

#### **Stage 10: Basic Flexible Window (15 Questions)**

**Q7.1: Expand Window Until Sum >= Target**
```
Problem: Find first window where sum >= target
Input: arr = [1, 2, 3, 4, 5], target = 7
Output: Window [3, 4] (indices 2-3)

Solution:
def first_window_above_target(arr, target):
    window_sum = 0
    left = 0
    
    for right in range(len(arr)):
        window_sum += arr[right]
        
        if window_sum >= target:
            return arr[left:right+1]
    
    return []
```

**Q7.2: Smallest Subarray Sum >= S**
```
Problem: Find length of smallest subarray with sum >= S
Input: arr = [2, 1, 5, 2, 3, 2], S = 7
Output: 2 (subarray [5, 2])

Solution:
def smallest_subarray_sum(arr, S):
    min_length = float('inf')
    window_sum = 0
    left = 0
    
    for right in range(len(arr)):
        window_sum += arr[right]
        
        # Shrink window while sum >= S
        while window_sum >= S:
            min_length = min(min_length, right - left + 1)
            window_sum -= arr[left]
            left += 1
    
    return min_length if min_length != float('inf') else 0
```

**Q7.3: Largest Subarray Sum <= S**
```
Problem: Find length of largest subarray with sum <= S
Input: arr = [1, 2, 3, 4, 5], S = 7
Output: 3 (subarray [1, 2, 3])

Solution:
def largest_subarray_sum_at_most(arr, S):
    max_length = 0
    window_sum = 0
    left = 0
    
    for right in range(len(arr)):
        window_sum += arr[right]
        
        # Shrink if sum exceeds S
        while window_sum > S:
            window_sum -= arr[left]
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

**Q7.4: Count Subarrays with Sum Exactly K**
```
Problem: Count subarrays with sum equal to K
Input: arr = [1, 2, 1, 2, 1], K = 3
Output: 4

Solution (using prefix sum):
def count_subarrays_sum_k(arr, K):
    count = 0
    prefix_sum = 0
    sum_map = {0: 1}
    
    for num in arr:
        prefix_sum += num
        
        if prefix_sum - K in sum_map:
            count += sum_map[prefix_sum - K]
        
        sum_map[prefix_sum] = sum_map.get(prefix_sum, 0) + 1
    
    return count
```

**Q7.5: Longest Substring with At Most K Distinct Characters**
```
Problem: Find length of longest substring with <= K distinct chars
Input: s = "araaci", K = 2
Output: 4 (substring "araa")

Solution:
def longest_substring_k_distinct(s, K):
    max_length = 0
    char_freq = {}
    left = 0
    
    for right in range(len(s)):
        # Expand: Add character
        char_freq[s[right]] = char_freq.get(s[right], 0) + 1
        
        # Shrink: While more than K distinct
        while len(char_freq) > K:
            char_freq[s[left]] -= 1
            if char_freq[s[left]] == 0:
                del char_freq[s[left]]
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

**Q7.6: Longest Substring with Exactly K Distinct Characters**
```
Problem: Exactly K distinct (not at most)
Input: s = "araaci", K = 2
Output: 4 (substring "araa")

Solution:
def longest_exactly_k_distinct(s, K):
    # at_most_k - at_most_(k-1) = exactly_k
    def at_most_k_distinct(s, K):
        max_length = 0
        char_freq = {}
        left = 0
        
        for right in range(len(s)):
            char_freq[s[right]] = char_freq.get(s[right], 0) + 1
            
            while len(char_freq) > K:
                char_freq[s[left]] -= 1
                if char_freq[s[left]] == 0:
                    del char_freq[s[left]]
                left += 1
            
            max_length = max(max_length, right - left + 1)
        
        return max_length
    
    return at_most_k_distinct(s, K) - at_most_k_distinct(s, K - 1)
```

**Q7.7: Longest Substring Without Repeating Characters**
```
Problem: Find longest substring with all unique characters
Input: "abcabcbb"
Output: 3 (substring "abc")

Solution:
def longest_unique_substring(s):
    max_length = 0
    char_set = set()
    left = 0
    
    for right in range(len(s)):
        # Shrink until character is unique
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        
        char_set.add(s[right])
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

**Q7.8: Longest Repeating Character Replacement (K Changes)**
```
Problem: Longest substring after replacing at most K characters
Input: s = "AABABBA", K = 1
Output: 4 (substring "AABA")

Solution:
def character_replacement(s, K):
    max_length = 0
    char_count = {}
    left = 0
    max_freq = 0
    
    for right in range(len(s)):
        char_count[s[right]] = char_count.get(s[right], 0) + 1
        max_freq = max(max_freq, char_count[s[right]])
        
        # Window size - most frequent > K means we need > K changes
        while (right - left + 1) - max_freq > K:
            char_count[s[left]] -= 1
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

**Q7.9: Maximum Consecutive Ones (After Flipping K Zeros)**
```
Problem: Max consecutive 1s after flipping at most K zeros
Input: arr = [1,1,0,0,1,1,1,0,1,1], K = 2
Output: 7

Solution:
def max_consecutive_ones(arr, K):
    max_length = 0
    zero_count = 0
    left = 0
    
    for right in range(len(arr)):
        if arr[right] == 0:
            zero_count += 1
        
        # Shrink if more than K zeros
        while zero_count > K:
            if arr[left] == 0:
                zero_count -= 1
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

**Q7.10: Minimum Window Substring**
```
Problem: Smallest substring containing all characters of pattern
Input: s = "ADOBECODEBANC", pattern = "ABC"
Output: "BANC"

Solution:
def min_window_substring(s, pattern):
    if not s or not pattern:
        return ""
    
    pattern_count = {}
    for char in pattern:
        pattern_count[char] = pattern_count.get(char, 0) + 1
    
    required = len(pattern_count)
    formed = 0
    window_counts = {}
    
    left = 0
    min_length = float('inf')
    min_left = 0
    
    for right in range(len(s)):
        char = s[right]
        window_counts[char] = window_counts.get(char, 0) + 1
        
        if char in pattern_count and window_counts[char] == pattern_count[char]:
            formed += 1
        
        # Shrink window
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
```

**Q7.11: Fruits Into Baskets (At Most 2 Types)**
```
Problem: Pick maximum fruits with at most 2 types
Input: fruits = [1,2,1,2,3,1,1]
Output: 5 (subarray [1,2,1,2,3] has 2 types, but actually [2,3,1,1,1] is invalid... correct is [1,2,1,2])

Actually: At most 2 distinct = longest_substring_k_distinct with K=2

Solution:
def total_fruits(fruits):
    return longest_substring_k_distinct(fruits, 2)

def longest_substring_k_distinct(arr, K):
    max_length = 0
    type_count = {}
    left = 0
    
    for right in range(len(arr)):
        type_count[arr[right]] = type_count.get(arr[right], 0) + 1
        
        while len(type_count) > K:
            type_count[arr[left]] -= 1
            if type_count[arr[left]] == 0:
                del type_count[arr[left]]
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

**Q7.12: Count Nice Subarrays (Exactly K Odd Numbers)**
```
Problem: Count subarrays with exactly K odd numbers
Input: arr = [1,1,2,1,1], K = 3
Output: 2

Solution:
def number_of_nice_subarrays(arr, K):
    def at_most_k_odds(arr, K):
        count = 0
        odd_count = 0
        left = 0
        
        for right in range(len(arr)):
            if arr[right] % 2 == 1:
                odd_count += 1
            
            while odd_count > K:
                if arr[left] % 2 == 1:
                    odd_count -= 1
                left += 1
            
            count += right - left + 1
        
        return count
    
    return at_most_k_odds(arr, K) - at_most_k_odds(arr, K - 1)
```

**Q7.13: Subarrays with Product Less Than K**
```
Problem: Count subarrays where product < K
Input: arr = [10, 5, 2, 6], K = 100
Output: 8

Solution:
def num_subarray_product_less_than_k(arr, K):
    if K <= 1:
        return 0
    
    count = 0
    product = 1
    left = 0
    
    for right in range(len(arr)):
        product *= arr[right]
        
        while product >= K:
            product //= arr[left]
            left += 1
        
        # All subarrays ending at right
        count += right - left + 1
    
    return count
```

**Q7.14: Longest Subarray with Sum At Most K**
```
Problem: Longest subarray with sum <= K
Input: arr = [1, 2, 3, 4, 5], K = 8
Output: 3

Solution:
def longest_subarray_sum_at_most_k(arr, K):
    max_length = 0
    window_sum = 0
    left = 0
    
    for right in range(len(arr)):
        window_sum += arr[right]
        
        while window_sum > K:
            window_sum -= arr[left]
            left += 1
        
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

**Q7.15: Longest Substring with Same Letters (After K Replacements)**
```
Problem: Already covered in Q7.8
This is same as Character Replacement problem
```

---

## 🔥 PATTERN 5: SPECIAL TECHNIQUES

### 🎓 Stage 11: Advanced Problems (10 Questions)

**Q8.1: Three Sum (3 Pointers)**
```
Problem: Find all unique triplets that sum to zero
Input: [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]

Solution:
def three_sum(arr):
    arr.sort()
    result = []
    
    for i in range(len(arr) - 2):
        # Skip duplicates for first element
        if i > 0 and arr[i] == arr[i-1]:
            continue
        
        left, right = i + 1, len(arr) - 1
        
        while left < right:
            total = arr[i] + arr[left] + arr[right]
            
            if total == 0:
                result.append([arr[i], arr[left], arr[right]])
                
                # Skip duplicates for second element
                while left < right and arr[left] == arr[left+1]:
                    left += 1
                # Skip duplicates for third element
                while left < right and arr[right] == arr[right-1]:
                    right -= 1
                
                left += 1
                right -= 1
            elif total < 0:
                left += 1
            else:
                right -= 1
    
    return result
```

**Q8.2: Four Sum**
```
Problem: Find all quadruplets that sum to target
Input: arr = [1, 0, -1, 0, -2, 2], target = 0
Output: [[-2,-1,1,2], [-2,0,0,2], [-1,0,0,1]]

Solution:
def four_sum(arr, target):
    arr.sort()
    result = []
    n = len(arr)
    
    for i in range(n - 3):
        if i > 0 and arr[i] == arr[i-1]:
            continue
        
        for j in range(i + 1, n - 2):
            if j > i + 1 and arr[j] == arr[j-1]:
                continue
            
            left, right = j + 1, n - 1
            
            while left < right:
                total = arr[i] + arr[j] + arr[left] + arr[right]
                
                if total == target:
                    result.append([arr[i], arr[j], arr[left], arr[right]])
                    
                    while left < right and arr[left] == arr[left+1]:
                        left += 1
                    while left < right and arr[right] == arr[right-1]:
                        right -= 1
                    
                    left += 1
                    right -= 1
                elif total < target:
                    left += 1
                else:
                    right -= 1
    
    return result
```

**Q8.3: Trapping Rain Water**
```
Problem: Calculate trapped rainwater
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6

Solution:
def trap_rain_water(height):
    if not height:
        return 0
    
    left, right = 0, len(height) - 1
    left_max, right_max = 0, 0
    water = 0
    
    while left < right:
        if height[left] < height[right]:
            if height[left] >= left_max:
                left_max = height[left]
            else:
                water += left_max - height[left]
            left += 1
        else:
            if height[right] >= right_max:
                right_max = height[right]
            else:
                water += right_max - height[right]
            right -= 1
    
    return water
```

**Q8.4: Sort Colors (Dutch National Flag)**
```
Already covered in Q5.23
```

**Q8.5: Partition Array Into Three Parts Equal Sum**
```
Problem: Can array be divided into 3 parts with equal sum?
Input: [0,2,1,-6,6,-7,9,1,2,0,1]
Output: True

Solution:
def can_three_parts_equal_sum(arr):
    total_sum = sum(arr)
    
    if total_sum % 3 != 0:
        return False
    
    target = total_sum // 3
    count = 0
    current_sum = 0
    
    for i in range(len(arr)):
        current_sum += arr[i]
        
        if current_sum == target:
            count += 1
            current_sum = 0
    
    return count >= 3
```

**Q8.6: 3Sum Closest**
```
Problem: Find three numbers whose sum is closest to target
Input: arr = [-1, 2, 1, -4], target = 1
Output: 2 (from -1 + 2 + 1)

Solution:
def three_sum_closest(arr, target):
    arr.sort()
    closest_sum = float('inf')
    
    for i in range(len(arr) - 2):
        left, right = i + 1, len(arr) - 1
        
        while left < right:
            current_sum = arr[i] + arr[left] + arr[right]
            
            if abs(target - current_sum) < abs(target - closest_sum):
                closest_sum = current_sum
            
            if current_sum < target:
                left += 1
            elif current_sum > target:
                right -= 1
            else:
                return current_sum
    
    return closest_sum
```

**Q8.7: Squares of Sorted Array**
```
Already covered in Q5.22
```

**Q8.8: Merge Two Sorted Arrays**
```
Problem: Merge two sorted arrays into one
Input: arr1 = [1,3,5], arr2 = [2,4,6]
Output: [1,2,3,4,5,6]

Solution:
def merge_sorted_arrays(arr1, arr2):
    result = []
    i, j = 0, 0
    
    while i < len(arr1) and j < len(arr2):
        if arr1[i] <= arr2[j]:
            result.append(arr1[i])
            i += 1
        else:
            result.append(arr2[j])
            j += 1
    
    # Append remaining
    result.extend(arr1[i:])
    result.extend(arr2[j:])
    
    return result
```

**Q8.9: Intersection of Two Arrays**
```
Problem: Find common elements
Input: arr1 = [1,2,2,1], arr2 = [2,2]
Output: [2]

Solution:
def intersection(arr1, arr2):
    arr1.sort()
    arr2.sort()
    
    result = []
    i, j = 0, 0
    
    while i < len(arr1) and j < len(arr2):
        if arr1[i] == arr2[j]:
            if not result or result[-1] != arr1[i]:
                result.append(arr1[i])
            i += 1
            j += 1
        elif arr1[i] < arr2[j]:
            i += 1
        else:
            j += 1
    
    return result
```

**Q8.10: Backspace String Compare** ⭐
```
Already covered in Q5.25 - This is the problem you asked about!

Let me expand on it:

Problem: Given two strings with '#' as backspace, are they equal?
Input: s = "ab#c", t = "ad#c"
Output: True

WHY TWO POINTERS FROM END?
- Backspace affects characters BEFORE it
- Processing from end: we can skip characters that will be deleted
- Processing from start: we'd need extra space to build strings

DETAILED WALKTHROUGH:
s = "ab#c"
     ↑
Start from end, work backwards
- c: valid character
- #: backspace, so skip next character
- b: skipped (due to #)
- a: valid character
Result: "ac"

t = "ad#c"
- c: valid
- #: skip next
- d: skipped
- a: valid
Result: "ac"

Both = "ac", so True!

POINTER MANIPULATION TRICK:
1. Start from end of both strings
2. Count backspaces
3. Skip characters based on backspace count
4. Compare characters when both pointers at valid positions
5. Move backwards

The key insight: Working backwards lets us handle backspaces without building new strings!
```

---

## 🎯 PATTERN IDENTIFICATION GUIDE

### Quick Decision Framework:

```
START HERE
    ↓
Is array SORTED?
    ↓
   YES → Use OPPOSITE DIRECTION (left=0, right=n-1)
         Examples: Two Sum, Container With Water, Palindrome
    ↓
    NO → Continue...
    
Need to REMOVE/MODIFY elements?
    ↓
   YES → Use SAME DIRECTION (slow/fast)
         Examples: Remove duplicates, Move zeros
    ↓
    NO → Continue...
    
Looking for SUBARRAY/SUBSTRING?
    ↓
   YES → Is size FIXED?
         ↓
        YES → Use FIXED WINDOW
              Examples: Max sum K elements, Average
         ↓
         NO → Use FLEXIBLE WINDOW
              Examples: Longest substring, Min window
    ↓
    NO → Continue...
    
Need THREE elements?
    ↓
   YES → Use THREE POINTERS or Fixed + Two Pointers
         Examples: 3Sum, Sort Colors (Dutch Flag)
    ↓
    NO → Check if SPECIAL CASE
         Examples: Backspace (from end), Merge arrays
```

---

## 📝 PRACTICE ROUTINE

### Week 1: Foundation
- **Day 1-2**: Opposite Direction (Stage 1-2)
- **Day 3-4**: Opposite Direction (Stage 3-4)
- **Day 5**: Mixed review Level 1-4
- **Weekend**: Challenge yourself with new problems

### Week 2: Same Direction
- **Day 1-2**: Same Direction (Stage 5-6)
- **Day 3-4**: Same Direction (Stage 7)
- **Day 5**: Opposite + Same Direction mixed
- **Weekend**: Problem solving contest mode

### Week 3: Windows
- **Day 1-2**: Fixed Window (Stage 8-9)
- **Day 3-4**: Flexible Window (Stage 10)
- **Day 5**: All window problems
- **Weekend**: Hard problems

### Week 4: Mastery
- **Day 1-2**: Advanced techniques (Stage 11)
- **Day 3-4**: Mixed patterns
- **Day 5**: Speed solving (time yourself)
- **Weekend**: Mock interview problems

---

## 🔥 KEY INSIGHTS & TRICKS

### **Insight 1: Why Opposite Direction Works for Two Sum**
```
Sorted array: [1, 2, 3, 4, 6]
Target: 6

If sum is TOO SMALL: left++ (need bigger number)
If sum is TOO LARGE: right-- (need smaller number)

This works because array is SORTED!
```

### **Insight 2: Why Slow-Fast for Remove Duplicates**
```
[1, 1, 2, 2, 3]
 ↑
slow (last unique position)

 ↑  ↑
slow fast (fast finds next unique)

slow BUILDS the result
fast EXPLORES to find good elements
```

### **Insight 3: Sliding Window Optimization**
```
Brute force: Calculate sum for each window = O(n*k)
Sliding: Remove one, add one = O(n)

[1, 2, 3, 4, 5], k=3

Window 1: sum([1,2,3]) = 6
Window 2: 6 - 1 + 4 = 9  ← Just one subtraction and one addition!
```

### **Insight 4: When to Move Which Pointer**
```
OPPOSITE DIRECTION:
- Move to IMPROVE condition
- Move SMALLER value in container problem
- Move based on COMPARISON result

SAME DIRECTION:
- fast ALWAYS moves
- slow moves when CONDITION met

FLEXIBLE WINDOW:
- right ALWAYS expands
- left SHRINKS when condition violated
```

---

## 🎓 COMMON MISTAKES & FIXES

### Mistake 1: Infinite Loop
```python
# WRONG
while left < right:
    if condition:
        return True
    # Forgot to move pointers!

# CORRECT
while left < right:
    if condition:
        return True
    left += 1
    right -= 1
```

### Mistake 2: Index Out of Bounds
```python
# WRONG
while left <= len(arr):  # Off by one!
    print(arr[left])

# CORRECT
while left < len(arr):
    print(arr[left])
```

### Mistake 3: Wrong Window Size Calculation
```python
# WRONG
window_size = right - left  # Missing +1

# CORRECT
window_size = right - left + 1
```

### Mistake 4: Forgetting to Handle Edge Cases
```python
# WRONG
def remove_duplicates(arr):
    slow = 0
    for fast in range(1, len(arr)):  # Crashes if arr is empty!
        ...

# CORRECT
def remove_duplicates(arr):
    if not arr:  # Check empty
        return 0
    slow = 0
    for fast in range(1, len(arr)):
        ...
```

---

## 🏆 MASTERY CHECKLIST

- [ ] Can identify pattern from problem description
- [ ] Know when to use left-right vs slow-fast
- [ ] Understand why pointers move in each direction
- [ ] Can write code without looking at solutions
- [ ] Handle edge cases (empty, single element, all same)
- [ ] Optimize from brute force to two pointer
- [ ] Explain time/space complexity
- [ ] Solve problems in < 15 minutes (easy), < 30 (medium)

---

## 📚 SUMMARY

**100+ Micro-Questions organized by difficulty**
**5 Main Patterns with detailed tricks**
**Real problem-solving strategies**
**Pattern identification framework**
**Common mistakes and fixes**

**Master this guide = Master Two Pointers! 🚀**

Start with Stage 1, complete all exercises, and gradually progress. 

Practice daily, understand WHY each pointer moves, and soon you'll solve any two-pointer problem intuitively!
