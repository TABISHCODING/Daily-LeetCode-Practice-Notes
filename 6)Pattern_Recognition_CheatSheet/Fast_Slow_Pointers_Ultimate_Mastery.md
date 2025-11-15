# 🐢🐰 Fast & Slow Pointers Mastery Guide - Master the Hare and Tortoise

## 📘 Philosophy: Staircase Learning - Each Step is Independent

This guide teaches you **HOW TO THINK** with fast and slow pointers through 100+ micro-questions.
**Each stair is a tiny concept → Master all stairs → Final problem becomes trivial**

**Learning Method**: Like the famous race - the tortoise (slow) and hare (fast) working together to solve problems!

---

## 🧠 Core Fast & Slow Pointer Concepts

### **The 5 Fundamental Operations:**

1. **MOVE SLOW**: slow = slow.next (or slow += 1)
2. **MOVE FAST**: fast = fast.next.next (or fast += 2) 
3. **DETECT CYCLE**: Check if slow == fast
4. **FIND MIDDLE**: When fast reaches end, slow at middle
5. **FIND POSITION**: Use speed difference to locate elements

---

## 🎯 Main Use Cases

### **Use Case 1: LINKED LIST PROBLEMS**
- Detect cycles
- Find middle node
- Find cycle start
- Find Nth node from end
- Remove Nth node from end

### **Use Case 2: ARRAY PROBLEMS**  
- Find duplicate numbers
- Happy number problem
- Circular array loop

### **Use Case 3: SEQUENCE PROBLEMS**
- Check if linked list is palindrome
- Reorder list

---

## 📊 Pattern Breakdown with Staircase Questions

---

## 🟢 PART 1: BASIC FAST & SLOW MOVEMENT

### 🎓 STAIRCASE 1: Understanding Speed Difference (10 Micro-Steps)

**🪜 Step 1.1: What is Fast and Slow?**
```
Concept: Two pointers moving at different speeds

Array: [1, 2, 3, 4, 5, 6, 7, 8]

Step 1: slow=0, fast=0
Step 2: slow=1, fast=2 (fast moves 2 steps)
Step 3: slow=2, fast=4
Step 4: slow=3, fast=6
Step 5: slow=4, fast=8 (fast reaches end!)

Key: Fast moves TWICE as fast as slow
```

---

**🪜 Step 1.2: Print Slow and Fast Positions**
```
Problem: Track both pointers as they move through array
Input: [10, 20, 30, 40, 50, 60]
Output:
  Step 1: slow=0 (val=10), fast=0 (val=10)
  Step 2: slow=1 (val=20), fast=2 (val=30)
  Step 3: slow=2 (val=30), fast=4 (val=50)
  Step 4: slow=3 (val=40), fast=6 (out of bounds)

Solution:
def track_fast_slow(arr):
    slow = fast = 0
    step = 1
    
    while fast < len(arr):
        print(f"Step {step}: slow={slow} (val={arr[slow]}), fast={fast} (val={arr[fast]})")
        slow += 1
        fast += 2
        step += 1
```

---

**🪜 Step 1.3: When Does Fast Reach End?**
```
Problem: Count steps until fast pointer reaches/exceeds array end
Input: [1, 2, 3, 4, 5, 6, 7, 8]
Output: 4 steps

Formula: Approximately len(arr) / 2 steps

Solution:
def count_steps_to_end(arr):
    slow = fast = 0
    steps = 0
    
    while fast < len(arr):
        slow += 1
        fast += 2
        steps += 1
    
    return steps

# Practice: [1, 2, 3, 4, 5] → 2 steps
```

---

**🪜 Step 1.4: Where is Slow When Fast Reaches End?**
```
Problem: Find slow pointer position when fast reaches end
Input: [1, 2, 3, 4, 5, 6, 7, 8, 9]

When fast=8 (end), slow=4 (MIDDLE!)

Key Insight: Slow reaches MIDDLE when fast reaches END

Solution:
def slow_when_fast_ends(arr):
    slow = fast = 0
    
    while fast < len(arr) - 1:
        slow += 1
        fast += 2
    
    return slow, arr[slow]

# This is how we find middle element!
```

---

**🪜 Step 1.5: Find Middle Element (Array)**
```
Problem: Use fast/slow to find middle of array
Input: [1, 2, 3, 4, 5]
Output: 3 (middle element)

Input: [1, 2, 3, 4, 5, 6]
Output: 4 (second middle for even length)

Solution:
def find_middle(arr):
    if not arr:
        return None
    
    slow = fast = 0
    
    # fast moves 2 steps, slow moves 1
    while fast < len(arr) - 1:
        slow += 1
        fast += 2
        if fast >= len(arr):
            break
    
    return arr[slow]

# Practice: [10, 20, 30, 40, 50, 60, 70]
```

---

**🪜 Step 1.6: Distance Between Fast and Slow**
```
Problem: Track distance between pointers at each step
Input: [1, 2, 3, 4, 5, 6, 7, 8]

Step 1: distance = 0 (both at 0)
Step 2: distance = 1 (slow=1, fast=2)
Step 3: distance = 2 (slow=2, fast=4)
Step 4: distance = 3 (slow=3, fast=6)

Pattern: Distance increases by 1 each step

Solution:
def track_distance(arr):
    slow = fast = 0
    distances = []
    
    while fast < len(arr):
        distances.append(fast - slow)
        slow += 1
        fast += 2
    
    return distances
```

---

**🪜 Step 1.7: Collect Elements at Slow Positions**
```
Problem: Collect all elements that slow pointer visits
Input: [10, 20, 30, 40, 50, 60]
Output: [10, 20, 30] (slow visits indices 0, 1, 2)

Solution:
def collect_slow_elements(arr):
    slow = fast = 0
    elements = []
    
    while fast < len(arr):
        elements.append(arr[slow])
        slow += 1
        fast += 2
    
    return elements
```

---

**🪜 Step 1.8: Collect Elements at Fast Positions**
```
Problem: Collect all elements that fast pointer visits
Input: [10, 20, 30, 40, 50, 60]
Output: [10, 30, 50] (fast visits indices 0, 2, 4)

Solution:
def collect_fast_elements(arr):
    slow = fast = 0
    elements = []
    
    while fast < len(arr):
        elements.append(arr[fast])
        slow += 1
        fast += 2
    
    return elements
```

---

**🪜 Step 1.9: When Do They Meet Again? (Circular)**
```
Problem: In circular array, when do fast and slow meet?
Concept: If array is circular, they will eventually meet!

Array (circular): [0, 1, 2, 3, 4] → [0, 1, 2, 3, 4, 0, 1, 2...]

This is the KEY to cycle detection!

We'll explore this deeply in next sections.
```

---

**🪜 Step 1.10: Different Speeds (Fast = 3x Slow)**
```
Problem: What if fast moves 3 positions at a time?
Input: [1, 2, 3, 4, 5, 6, 7, 8, 9]

Step 1: slow=0, fast=0
Step 2: slow=1, fast=3
Step 3: slow=2, fast=6
Step 4: slow=3, fast=9 (out)

Solution:
def different_speeds(arr):
    slow = fast = 0
    positions = []
    
    while fast < len(arr):
        positions.append((slow, fast))
        slow += 1
        fast += 3
    
    return positions

# Different speeds useful for different problems!
```

---

### 🎓 STAIRCASE 2: Linked List Basics (15 Micro-Steps)

**🪜 Step 2.1: Linked List Node Structure**
```
Concept: Understand linked list structure

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

Example: 1 → 2 → 3 → 4 → 5 → None

node1.val = 1
node1.next = node2
node2.val = 2
node2.next = node3
...
```

---

**🪜 Step 2.2: Traverse Linked List with One Pointer**
```
Problem: Print all values in linked list
Input: 1 → 2 → 3 → 4 → None
Output: 1, 2, 3, 4

Solution:
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def traverse(head):
    current = head
    while current:
        print(current.val, end=" ")
        current = current.next
```

---

**🪜 Step 2.3: Count Nodes in Linked List**
```
Problem: Count total nodes
Input: 1 → 2 → 3 → 4 → 5 → None
Output: 5

Solution:
def count_nodes(head):
    count = 0
    current = head
    
    while current:
        count += 1
        current = current.next
    
    return count
```

---

**🪜 Step 2.4: Move Two Pointers in Linked List**
```
Problem: Move slow 1 step, fast 2 steps in linked list
Input: 1 → 2 → 3 → 4 → 5 → None

Step 1: slow=1, fast=1
Step 2: slow=2, fast=3
Step 3: slow=3, fast=5
Step 4: slow=4, fast=None

Solution:
def move_two_pointers(head):
    slow = fast = head
    
    while fast and fast.next:
        print(f"slow={slow.val}, fast={fast.val}")
        slow = slow.next
        fast = fast.next.next
```

---

**🪜 Step 2.5: Find Middle of Linked List** ⭐ **LeetCode #876**
```
Problem: Find middle node of linked list
Input: 1 → 2 → 3 → 4 → 5 → None
Output: 3

Input: 1 → 2 → 3 → 4 → None
Output: 3 (second middle for even length)

Solution:
def middleNode(head):
    slow = fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    return slow

# LeetCode #876: Middle of the Linked List
# When fast reaches end, slow is at middle!
```

---

**🪜 Step 2.6: Find 1/3 Position in Linked List**
```
Problem: Find node at 1/3 position
Input: 1 → 2 → 3 → 4 → 5 → 6 → None
Output: 2 (node at position 2, which is 6/3=2)

Solution:
def find_one_third(head):
    slow = fast = head
    
    # Fast moves 3 times as fast
    while fast and fast.next and fast.next.next:
        slow = slow.next
        fast = fast.next.next.next
    
    return slow

# By changing speed ratio, we can find different positions!
```

---

**🪜 Step 2.7: Check if List Has Even or Odd Length**
```
Problem: Determine if linked list has even or odd number of nodes
Input: 1 → 2 → 3 → 4 → None
Output: "Even" (4 nodes)

Solution:
def is_even_length(head):
    fast = head
    
    while fast and fast.next:
        fast = fast.next.next
    
    # If fast is None, even length
    # If fast.next is None, odd length
    return fast is None

# Even: fast ends at None
# Odd: fast ends at last node
```

---

**🪜 Step 2.8: Find Nth Node from Beginning**
```
Problem: Find nth node from start (using fast/slow concept)
Input: 1 → 2 → 3 → 4 → 5 → None, n=3
Output: 3

Solution:
def find_nth_from_start(head, n):
    current = head
    
    for _ in range(n - 1):
        if not current:
            return None
        current = current.next
    
    return current

# Not really fast/slow, but foundation for next problem
```

---

**🪜 Step 2.9: Find Nth Node from End** ⭐ **LeetCode #19 Pattern**
```
Problem: Find nth node from end of linked list
Input: 1 → 2 → 3 → 4 → 5 → None, n=2
Output: 4 (second from end)

Technique: Give fast a head start of n nodes!

Solution:
def find_nth_from_end(head, n):
    fast = slow = head
    
    # Move fast n steps ahead
    for _ in range(n):
        if not fast:
            return None
        fast = fast.next
    
    # Move both until fast reaches end
    while fast:
        slow = slow.next
        fast = fast.next
    
    return slow

# When fast reaches end, slow is n steps from end!
```

---

**🪜 Step 2.10: Remove Nth Node from End** ⭐ **LeetCode #19**
```
Problem: Remove nth node from end of linked list
Input: 1 → 2 → 3 → 4 → 5 → None, n=2
Output: 1 → 2 → 3 → 5 → None (removed 4)

Solution:
def removeNthFromEnd(head, n):
    dummy = ListNode(0)
    dummy.next = head
    fast = slow = dummy
    
    # Move fast n+1 steps ahead
    for _ in range(n + 1):
        fast = fast.next
    
    # Move both until fast reaches end
    while fast:
        slow = slow.next
        fast = fast.next
    
    # Remove node
    slow.next = slow.next.next
    
    return dummy.next

# LeetCode #19: Remove Nth Node From End of List
# Use dummy node to handle edge case of removing head
```

---

**🪜 Step 2.11: Split List into Two Halves**
```
Problem: Split linked list into two equal halves
Input: 1 → 2 → 3 → 4 → 5 → 6 → None
Output: First half: 1 → 2 → 3, Second half: 4 → 5 → 6

Solution:
def split_list(head):
    if not head:
        return None, None
    
    slow = fast = head
    prev = None
    
    while fast and fast.next:
        prev = slow
        slow = slow.next
        fast = fast.next.next
    
    # Break the link
    if prev:
        prev.next = None
    
    return head, slow

# First half: head to prev
# Second half: slow to end
```

---

**🪜 Step 2.12: Compare Two Lists at Same Speed**
```
Problem: Check if two lists are identical
Input: List1: 1 → 2 → 3, List2: 1 → 2 → 3
Output: True

Solution:
def are_identical(head1, head2):
    p1, p2 = head1, head2
    
    while p1 and p2:
        if p1.val != p2.val:
            return False
        p1 = p1.next
        p2 = p2.next
    
    # Both should reach None together
    return p1 is None and p2 is None
```

---

**🪜 Step 2.13: Reverse First Half of List**
```
Problem: Reverse first half of linked list
Input: 1 → 2 → 3 → 4 → 5 → 6 → None
Output: 3 → 2 → 1 → 4 → 5 → 6 → None

Solution:
def reverse_first_half(head):
    # Find middle
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    # Reverse first half (up to slow)
    prev = None
    current = head
    
    while current != slow:
        next_node = current.next
        current.next = prev
        prev = current
        current = next_node
    
    # Connect reversed part to second half
    head.next = slow
    
    return prev
```

---

**🪜 Step 2.14: Check if List is Palindrome** ⭐ **LeetCode #234**
```
Problem: Check if linked list is palindrome
Input: 1 → 2 → 2 → 1 → None
Output: True

Input: 1 → 2 → 3 → None
Output: False

Technique:
1. Find middle (fast/slow)
2. Reverse second half
3. Compare first and second halves

Solution:
def isPalindrome(head):
    if not head or not head.next:
        return True
    
    # Find middle
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    # Reverse second half
    prev = None
    while slow:
        next_node = slow.next
        slow.next = prev
        prev = slow
        slow = next_node
    
    # Compare
    left, right = head, prev
    while right:  # right is shorter or equal
        if left.val != right.val:
            return False
        left = left.next
        right = right.next
    
    return True

# LeetCode #234: Palindrome Linked List
# Classic fast/slow application!
```

---

**🪜 Step 2.15: Reorder List** ⭐ **LeetCode #143**
```
Problem: Reorder list as L0→Ln→L1→Ln-1→L2→Ln-2...
Input: 1 → 2 → 3 → 4 → None
Output: 1 → 4 → 2 → 3 → None

Input: 1 → 2 → 3 → 4 → 5 → None
Output: 1 → 5 → 2 → 4 → 3 → None

Technique:
1. Find middle (fast/slow)
2. Reverse second half
3. Merge two halves alternately

Solution:
def reorderList(head):
    if not head or not head.next:
        return
    
    # Find middle
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    # Reverse second half
    prev, curr = None, slow
    while curr:
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node
    
    # Merge two halves
    first, second = head, prev
    while second.next:
        tmp1, tmp2 = first.next, second.next
        first.next = second
        second.next = tmp1
        first, second = tmp1, tmp2

# LeetCode #143: Reorder List
# Combines: find middle + reverse + merge
```

---

### 🎓 STAIRCASE 3: Cycle Detection (20 Micro-Steps)

**🪜 Step 3.1: What is a Cycle?**
```
Concept: When a node points back to a previous node

Example:
1 → 2 → 3 → 4 → 5
        ↑       ↓
        ← ← ← ← ←

Node 5 points back to Node 3, creating a cycle!

No cycle: All nodes eventually reach None
With cycle: Nodes loop infinitely
```

---

**🪜 Step 3.2: Why Fast & Slow Detects Cycles?**
```
Concept: If there's a cycle, fast will eventually catch slow!

Think: Running on a circular track
- Slow runner: 1 lap per minute
- Fast runner: 2 laps per minute

Eventually fast will lap slow and they'll meet!

In linked list:
- Slow: moves 1 node per step
- Fast: moves 2 nodes per step
- In cycle: Fast catches up to slow
```

---

**🪜 Step 3.3: Detect Cycle (Basic)** ⭐ **LeetCode #141**
```
Problem: Detect if linked list has a cycle
Input: 1 → 2 → 3 → 4 → 2 (cycle back to node 2)
Output: True

Input: 1 → 2 → 3 → None
Output: False

Solution:
def hasCycle(head):
    if not head or not head.next:
        return False
    
    slow = fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:  # They met - cycle exists!
            return True
    
    return False  # Fast reached end - no cycle

# LeetCode #141: Linked List Cycle
# MOST FAMOUS fast/slow pointer problem!
```

---

**🪜 Step 3.4: Where Do They Meet?**
```
Problem: Find the node where fast and slow meet in a cycle

Example:
1 → 2 → 3 → 4 → 5
        ↑       ↓
        ← ← ← ← ←

Let's trace:
Start: slow=1, fast=1
Step 1: slow=2, fast=3
Step 2: slow=3, fast=5
Step 3: slow=4, fast=4 (MEET!)

They meet at node 4 (not necessarily the cycle start!)

Solution:
def find_meeting_point(head):
    if not head or not head.next:
        return None
    
    slow = fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            return slow  # Return meeting node
    
    return None
```

---

**🪜 Step 3.5: Find Cycle Start** ⭐ **LeetCode #142**
```
Problem: Find the node where cycle begins
Input: 1 → 2 → 3 → 4 → 5 → 3 (cycle starts at 3)
Output: Node 3

Magic Formula (Floyd's Algorithm):
1. Detect cycle and find meeting point
2. Move one pointer to head
3. Move both at SAME speed
4. Where they meet = cycle start!

Why this works? Mathematics! (see explanation below)

Solution:
def detectCycle(head):
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
    slow = head  # Reset slow to head
    
    while slow != fast:
        slow = slow.next
        fast = fast.next  # Both move at same speed!
    
    return slow  # This is the cycle start!

# LeetCode #142: Linked List Cycle II
# Floyd's Cycle Detection Algorithm
```

---

**🪜 Step 3.6: Why Does Floyd's Algorithm Work?**
```
Mathematical Proof:

Let:
- L = distance from head to cycle start
- C = cycle length
- K = distance from cycle start to meeting point

When they meet:
- Slow traveled: L + K
- Fast traveled: L + K + nC (n = number of complete cycles)

Since fast is 2x speed of slow:
2(L + K) = L + K + nC
2L + 2K = L + K + nC
L + K = nC
L = nC - K

This means:
Distance from head to cycle start (L) = 
Distance from meeting point to cycle start (C - K)

That's why moving both at same speed makes them meet at cycle start!

Beautiful mathematics! 🎓
```

---

**🪜 Step 3.7: Find Cycle Length**
```
Problem: Find length of the cycle
Input: 1 → 2 → 3 → 4 → 5 → 3 (cycle: 3→4→5→3)
Output: 3 (cycle has 3 nodes)

Technique:
1. Detect cycle and find meeting point
2. Keep fast at meeting point, move slow
3. Count steps until slow meets fast again

Solution:
def find_cycle_length(head):
    if not head or not head.next:
        return 0
    
    # Detect cycle
    slow = fast = head
    has_cycle = False
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            has_cycle = True
            break
    
    if not has_cycle:
        return 0
    
    # Count cycle length
    count = 1
    current = slow.next
    
    while current != slow:
        count += 1
        current = current.next
    
    return count
```

---

**🪜 Step 3.8: Find Node Before Cycle Start**
```
Problem: Find the last node before cycle begins
Input: 1 → 2 → 3 → 4 → 5 → 3
Output: Node 2 (points to cycle start 3)

Solution:
def node_before_cycle(head):
    # First find cycle start
    cycle_start = detectCycle(head)
    
    if not cycle_start:
        return None
    
    # Traverse from head to find node pointing to cycle_start
    current = head
    
    while current.next != cycle_start:
        current = current.next
    
    return current
```

---

**🪜 Step 3.9: Remove Cycle from List**
```
Problem: Break the cycle in linked list
Input: 1 → 2 → 3 → 4 → 5 → 3
Output: 1 → 2 → 3 → 4 → 5 → None

Solution:
def remove_cycle(head):
    # Find cycle start
    cycle_start = detectCycle(head)
    
    if not cycle_start:
        return head  # No cycle
    
    # Find node that points to cycle_start
    current = cycle_start
    
    while current.next != cycle_start:
        current = current.next
    
    # Break the cycle
    current.next = None
    
    return head
```

---

**🪜 Step 3.10: Circular Array Cycle** ⭐ **LeetCode #457**
```
Problem: Detect cycle in circular array
Input: [2, -1, 1, 2, 2]
Output: True

Each nums[i] represents steps to jump

Solution:
def circularArrayLoop(nums):
    n = len(nums)
    
    def next_index(i):
        return (i + nums[i]) % n
    
    for i in range(n):
        slow = fast = i
        forward = nums[i] > 0
        
        while True:
            # Move slow one step
            slow = next_index(slow)
            
            # Check direction
            if (nums[slow] > 0) != forward:
                break
            
            # Move fast two steps
            fast = next_index(fast)
            if (nums[fast] > 0) != forward:
                break
            
            fast = next_index(fast)
            if (nums[fast] > 0) != forward:
                break
            
            # Cycle detected
            if slow == fast:
                # Check if cycle length > 1
                if slow == next_index(slow):
                    break
                return True
        
    return False

# LeetCode #457: Circular Array Loop
```

---

**🪜 Step 3.11: Happy Number** ⭐ **LeetCode #202**
```
Problem: Determine if number is "happy"
A happy number: sum of squares of digits eventually = 1

Input: 19
1² + 9² = 82
8² + 2² = 68
6² + 8² = 100
1² + 0² + 0² = 1 ← Happy!

Input: 2
2² = 4
4² = 16
1² + 6² = 37
3² + 7² = 58
5² + 8² = 89
8² + 9² = 145
1² + 4² + 5² = 42
4² + 2² = 20
2² + 0² = 4 ← Cycle! Not happy.

Use Fast/Slow to detect cycle!

Solution:
def isHappy(n):
    def get_next(num):
        total = 0
        while num > 0:
            digit = num % 10
            total += digit * digit
            num //= 10
        return total
    
    slow = n
    fast = n
    
    while True:
        slow = get_next(slow)
        fast = get_next(get_next(fast))
        
        if fast == 1:
            return True
        
        if slow == fast:  # Cycle detected
            return False

# LeetCode #202: Happy Number
# Brilliant use of cycle detection!
```

---

**🪜 Step 3.12: Find Duplicate Number** ⭐ **LeetCode #287**
```
Problem: Find duplicate in array of n+1 integers (range 1 to n)
Input: [1, 3, 4, 2, 2]
Output: 2

Input: [3, 1, 3, 4, 2]
Output: 3

Constraint: Don't modify array, O(1) space

Brilliant Insight: Treat array as linked list!
nums[i] is "next pointer"

Example: [1, 3, 4, 2, 2]
Index:    0  1  2  3  4
Value:    1  3  4  2  2

0 → 1 → 3 → 2 → 4 → 2 (cycle!)
                ↑______|

The duplicate creates a cycle!

Solution:
def findDuplicate(nums):
    # Phase 1: Detect cycle
    slow = fast = nums[0]
    
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            break
    
    # Phase 2: Find cycle start (the duplicate)
    slow = nums[0]
    
    while slow != fast:
        slow = nums[slow]
        fast = nums[fast]
    
    return slow

# LeetCode #287: Find the Duplicate Number
# Mind-blowing application of Floyd's algorithm!
```

---

**🪜 Step 3.13: Start of Duplicate Sequence**
```
Problem: Find where duplicate sequence starts in array
Input: [1, 2, 3, 3, 3, 4, 5]
Output: Index 2 (first 3)

This is finding cycle start in array context

Solution:
def start_of_duplicates(arr):
    if len(arr) < 2:
        return -1
    
    for i in range(len(arr) - 1):
        if arr[i] == arr[i + 1]:
            # Found start of duplicate
            return i
    
    return -1  # No duplicates
```

---

**🪜 Step 3.14: Cycle in Directed Graph**
```
Problem: Detect cycle in directed graph
Use DFS with fast/slow concept for some variants

This extends beyond linked lists!

Solution (using graph):
def has_cycle_graph(graph):
    visited = set()
    rec_stack = set()
    
    def dfs(node):
        visited.add(node)
        rec_stack.add(node)
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                if dfs(neighbor):
                    return True
            elif neighbor in rec_stack:
                return True  # Cycle detected
        
        rec_stack.remove(node)
        return False
    
    for node in graph:
        if node not in visited:
            if dfs(node):
                return True
    
    return False
```

---

**🪜 Step 3.15: Cycle Detection in String**
```
Problem: Detect repeating pattern in string
Input: "abcabcabc"
Output: True (pattern "abc" repeats)

Solution:
def has_pattern_cycle(s):
    n = len(s)
    
    for length in range(1, n // 2 + 1):
        if n % length == 0:
            pattern = s[:length]
            if pattern * (n // length) == s:
                return True
    
    return False

# Not traditional fast/slow but same cycle concept
```

---

**🪜 Step 3.16-3.20: Advanced Cycle Problems**

**🪜 Step 3.16**: Find All Cycles in Graph
**🪜 Step 3.17**: Longest Cycle in Graph
**🪜 Step 3.18**: Count Nodes Not in Cycle
**🪜 Step 3.19**: Cycle in 2D Grid (LeetCode #1559)
**🪜 Step 3.20**: Redundant Connection (LeetCode #684)

---

### 🎓 STAIRCASE 4: Advanced Applications (15 Micro-Steps)

**🪜 Step 4.1: Sort List** ⭐ **LeetCode #148**
```
Problem: Sort linked list using merge sort
Input: 4 → 2 → 1 → 3 → None
Output: 1 → 2 → 3 → 4 → None

Use fast/slow to find middle for merge sort!

Solution:
def sortList(head):
    if not head or not head.next:
        return head
    
    # Find middle using fast/slow
    slow = fast = head
    prev = None
    
    while fast and fast.next:
        prev = slow
        slow = slow.next
        fast = fast.next.next
    
    # Split list
    prev.next = None
    
    # Recursively sort both halves
    left = sortList(head)
    right = sortList(slow)
    
    # Merge sorted halves
    return merge(left, right)

def merge(l1, l2):
    dummy = ListNode(0)
    current = dummy
    
    while l1 and l2:
        if l1.val < l2.val:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next
    
    current.next = l1 or l2
    return dummy.next

# LeetCode #148: Sort List
# Merge sort uses fast/slow to find middle!
```

---

**🪜 Step 4.2: Intersection of Two Linked Lists** ⭐ **LeetCode #160**
```
Problem: Find node where two lists intersect
Input:
  A: 1 → 2 → 3
              ↘
                7 → 8 → 9
              ↗
  B: 4 → 5 → 6

Output: Node 7

Technique: Two pointers at same speed!
When p1 reaches end, restart at head of B
When p2 reaches end, restart at head of A
They'll meet at intersection!

Solution:
def getIntersectionNode(headA, headB):
    if not headA or not headB:
        return None
    
    p1, p2 = headA, headB
    
    while p1 != p2:
        # Move to next or switch to other list
        p1 = p1.next if p1 else headB
        p2 = p2.next if p2 else headA
    
    return p1  # Either intersection or None

# LeetCode #160: Intersection of Two Linked Lists
# Clever use of two pointers!
```

---

**🪜 Step 4.3: Add Two Numbers II** ⭐ **LeetCode #445**
```
Problem: Add two numbers represented as linked lists
Input: 7 → 2 → 4 → 3 (represents 7243)
       5 → 6 → 4 (represents 564)
Output: 7 → 8 → 0 → 7 (represents 7807)

Use fast/slow to reverse or find lengths!

Solution:
def addTwoNumbers(l1, l2):
    # Reverse both lists
    l1 = reverse_list(l1)
    l2 = reverse_list(l2)
    
    dummy = ListNode(0)
    current = dummy
    carry = 0
    
    while l1 or l2 or carry:
        val1 = l1.val if l1 else 0
        val2 = l2.val if l2 else 0
        
        total = val1 + val2 + carry
        carry = total // 10
        current.next = ListNode(total % 10)
        
        current = current.next
        if l1: l1 = l1.next
        if l2: l2 = l2.next
    
    # Reverse result
    return reverse_list(dummy.next)

def reverse_list(head):
    prev = None
    while head:
        next_node = head.next
        head.next = prev
        prev = head
        head = next_node
    return prev

# LeetCode #445: Add Two Numbers II
```

---

**🪜 Step 4.4: Rotate List** ⭐ **LeetCode #61**
```
Problem: Rotate list to the right by k places
Input: 1 → 2 → 3 → 4 → 5, k=2
Output: 4 → 5 → 1 → 2 → 3

Use fast/slow to find rotation point!

Solution:
def rotateRight(head, k):
    if not head or not head.next or k == 0:
        return head
    
    # Find length
    length = 1
    tail = head
    while tail.next:
        tail = tail.next
        length += 1
    
    # Normalize k
    k = k % length
    if k == 0:
        return head
    
    # Find new tail (length - k - 1 from head)
    fast = slow = head
    
    # Move fast k steps ahead
    for _ in range(k):
        fast = fast.next
    
    # Move both until fast reaches end
    while fast.next:
        slow = slow.next
        fast = fast.next
    
    # Rotate
    new_head = slow.next
    slow.next = None
    fast.next = head
    
    return new_head

# LeetCode #61: Rotate List
```

---

**🪜 Step 4.5: Swap Nodes in Pairs** ⭐ **LeetCode #24**
```
Problem: Swap every two adjacent nodes
Input: 1 → 2 → 3 → 4 → None
Output: 2 → 1 → 4 → 3 → None

Solution:
def swapPairs(head):
    dummy = ListNode(0)
    dummy.next = head
    prev = dummy
    
    while prev.next and prev.next.next:
        # Nodes to swap
        first = prev.next
        second = prev.next.next
        
        # Swap
        first.next = second.next
        second.next = first
        prev.next = second
        
        # Move to next pair
        prev = first
    
    return dummy.next

# LeetCode #24: Swap Nodes in Pairs
```

---

**🪜 Step 4.6: Odd Even Linked List** ⭐ **LeetCode #328**
```
Problem: Group odd and even positioned nodes
Input: 1 → 2 → 3 → 4 → 5 → None
Output: 1 → 3 → 5 → 2 → 4 → None

Solution:
def oddEvenList(head):
    if not head or not head.next:
        return head
    
    odd = head
    even = head.next
    even_head = even
    
    while even and even.next:
        odd.next = even.next
        odd = odd.next
        even.next = odd.next
        even = even.next
    
    odd.next = even_head
    
    return head

# LeetCode #328: Odd Even Linked List
# Use two pointers moving at different rates!
```

---

**🪜 Step 4.7: Split Linked List in Parts** ⭐ **LeetCode #725**
```
Problem: Split list into k parts
Input: 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10, k=3
Output: [[1,2,3,4], [5,6,7], [8,9,10]]

Solution:
def splitListToParts(head, k):
    # Find length
    length = 0
    current = head
    while current:
        length += 1
        current = current.next
    
    # Calculate part sizes
    part_size = length // k
    extra = length % k
    
    result = []
    current = head
    
    for i in range(k):
        part_head = current
        current_size = part_size + (1 if i < extra else 0)
        
        # Move to end of current part
        for j in range(current_size - 1):
            if current:
                current = current.next
        
        # Break link
        if current:
            next_part = current.next
            current.next = None
            current = next_part
        
        result.append(part_head)
    
    return result

# LeetCode #725: Split Linked List in Parts
```

---

**🪜 Step 4.8: Design Circular Queue** ⭐ **LeetCode #622**
```
Problem: Implement circular queue using array/list

This uses circular concept like cycle detection!

Solution:
class MyCircularQueue:
    def __init__(self, k):
        self.queue = [0] * k
        self.size = k
        self.front = 0
        self.rear = -1
        self.count = 0
    
    def enQueue(self, value):
        if self.isFull():
            return False
        self.rear = (self.rear + 1) % self.size
        self.queue[self.rear] = value
        self.count += 1
        return True
    
    def deQueue(self):
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.size
        self.count -= 1
        return True
    
    def Front(self):
        return -1 if self.isEmpty() else self.queue[self.front]
    
    def Rear(self):
        return -1 if self.isEmpty() else self.queue[self.rear]
    
    def isEmpty(self):
        return self.count == 0
    
    def isFull(self):
        return self.count == self.size

# LeetCode #622: Design Circular Queue
```

---

**🪜 Step 4.9-4.15: More Advanced Problems**

**🪜 Step 4.9**: Reverse Nodes in k-Group (LeetCode #25 - Hard)
**🪜 Step 4.10**: Copy List with Random Pointer (LeetCode #138)
**🪜 Step 4.11**: Flatten Multilevel Doubly Linked List (LeetCode #430)
**🪜 Step 4.12**: Convert Binary Search Tree to Sorted Doubly Linked List (LeetCode #426)
**🪜 Step 4.13**: LRU Cache (LeetCode #146) - uses doubly linked list
**🪜 Step 4.14**: Design Browser History (LeetCode #1472)
**🪜 Step 4.15**: Maximum Twin Sum of Linked List (LeetCode #2130)

---

## 🎯 MASTERY CHECKLIST

### Basic Fast & Slow:
- [ ] Understand why fast moves 2x speed
- [ ] Can find middle of linked list
- [ ] Know when fast reaches end, slow at middle
- [ ] Can find nth node from end
- [ ] Handle even/odd length lists

### Cycle Detection:
- [ ] Understand Floyd's cycle detection
- [ ] Can detect if cycle exists
- [ ] Can find cycle start point
- [ ] Can calculate cycle length
- [ ] Know mathematical proof of why it works

### Advanced Applications:
- [ ] Can apply to arrays (treat as linked list)
- [ ] Recognize when to use fast/slow pattern
- [ ] Combine with other techniques (reverse, merge)
- [ ] Solve palindrome and reorder problems
- [ ] Handle complex variations

---

## 📊 LEETCODE PROBLEMS SUMMARY

### Easy:
1. **#876** - Middle of Linked List ⭐ FUNDAMENTAL
2. **#141** - Linked List Cycle ⭐ MOST FAMOUS
3. **#202** - Happy Number
4. **#160** - Intersection of Two Linked Lists

### Medium:
5. **#142** - Linked List Cycle II (Find start) ⭐ IMPORTANT
6. **#287** - Find Duplicate Number ⭐ BRILLIANT
7. **#19** - Remove Nth Node From End
8. **#234** - Palindrome Linked List
9. **#143** - Reorder List
10. **#148** - Sort List (Merge Sort)
11. **#328** - Odd Even Linked List
12. **#457** - Circular Array Loop
13. **#61** - Rotate List
14. **#24** - Swap Nodes in Pairs
15. **#445** - Add Two Numbers II
16. **#725** - Split Linked List in Parts
17. **#2130** - Maximum Twin Sum

### Hard:
18. **#25** - Reverse Nodes in k-Group

---

## 🚀 PRACTICE SCHEDULE

### Week 1: Basic Movement
- **Day 1-2**: Staircase 1 (Speed difference)
- **Day 3-4**: Staircase 2 (Linked list basics)
- **Day 5**: LeetCode #876, #19
- **Weekend**: Review and practice

### Week 2: Cycle Detection
- **Day 1-2**: Staircase 3 (Cycle basics)
- **Day 3**: LeetCode #141, #142 ⭐
- **Day 4**: LeetCode #202, #287
- **Day 5**: Review Floyd's algorithm proof
- **Weekend**: Mixed practice

### Week 3: Applications
- **Day 1**: LeetCode #234, #143
- **Day 2**: LeetCode #148, #328
- **Day 3**: LeetCode #160, #457
- **Day 4**: Review all patterns
- **Day 5**: Speed solving
- **Weekend**: Hard problems

---

## 💡 KEY PATTERNS

### Pattern 1: Find Middle
```python
slow = fast = head
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
# slow is at middle
```

### Pattern 2: Detect Cycle
```python
slow = fast = head
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
    if slow == fast:
        return True  # Cycle exists
return False
```

### Pattern 3: Find Cycle Start
```python
# After detecting cycle at meeting point
slow = head
while slow != fast:
    slow = slow.next
    fast = fast.next
return slow  # Cycle start
```

### Pattern 4: Nth from End
```python
fast = slow = head
# Move fast n steps ahead
for _ in range(n):
    fast = fast.next
# Move both together
while fast:
    slow = slow.next
    fast = fast.next
# slow is nth from end
```

---

## 🎓 WHY FAST & SLOW WORKS

### Mathematical Insight:
1. **Speed difference creates meeting**: Fast gains 1 position per step
2. **Cycle guarantee meeting**: In cycle, fast will lap slow
3. **Distance formula**: Meeting point math is predictable
4. **Floyd's brilliance**: Finding cycle start is pure mathematics

### Visual Understanding:
```
Think of a circular race track:
🐢 Tortoise: 1 step per second
🐰 Hare: 2 steps per second

On straight path: Hare reaches end while tortoise halfway
In circle: Hare eventually catches tortoise from behind
```

---

## ✅ STAIRCASE COMPLETION

- **Staircase 1**: Understand speed mechanics
- **Staircase 2**: Apply to linked lists
- **Staircase 3**: Master cycle detection
- **Staircase 4**: Advanced problems

**Complete all stairs → Solve any fast/slow problem → Interview success! 🎯**

---

**Start with Step 1.1 today and visualize the race between tortoise and hare! 🐢🐰**
