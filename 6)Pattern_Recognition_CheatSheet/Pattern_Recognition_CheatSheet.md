# DSA Pattern Recognition Cheat Sheet
## Quick Reference Guide for Identifying Patterns

---

## 🎯 Pattern Identification Framework

### Step 1: Analyze the Problem Statement

| Question | What to Look For | Likely Pattern |
|----------|------------------|----------------|
| What data structure? | Array, String, Tree, Graph, Matrix | Determines category |
| What's the goal? | Find, Count, Optimize, Generate | Determines approach |
| What are constraints? | Sorted, Unique, Range limits | Hints at optimization |
| Time/Space limits? | O(n), O(log n), O(1) space | Guides algorithm choice |

---

## 📋 Pattern Trigger Words Dictionary

### **Two Pointers**
**Trigger Words:**
- "Pair", "Triplet", "Quadruplet"
- "Sorted array/list"
- "Two numbers that sum to"
- "Remove duplicates in-place"
- "Palindrome"
- "Partition"
- "Compare from both ends"

**When to Use:**
- ✅ Array/string is sorted (or can be sorted)
- ✅ Finding pairs/combinations
- ✅ In-place modifications
- ✅ Comparing elements from different positions

**Time:** Usually O(n) or O(n²)  
**Space:** O(1)

---

### **Sliding Window**
**Trigger Words:**
- "Contiguous subarray/substring"
- "Maximum/minimum of size K"
- "Longest/shortest substring"
- "All subarrays of size K"
- "Window"
- "Consecutive elements"

**When to Use:**
- ✅ Contiguous sequence problems
- ✅ Finding optimal subarray/substring
- ✅ Running calculations (sum, avg)
- ✅ K distinct elements

**Time:** O(n)  
**Space:** O(k) for window contents

---

### **Fast & Slow Pointers**
**Trigger Words:**
- "Cycle in linked list"
- "Middle element"
- "Detect loop"
- "Happy number"
- "Find duplicate"
- "Circular"

**When to Use:**
- ✅ Linked list problems
- ✅ Cycle detection
- ✅ Finding middle/kth element
- ✅ Constant space requirement

**Time:** O(n)  
**Space:** O(1)

---

### **Prefix Sum**
**Trigger Words:**
- "Range sum query"
- "Subarray sum equals K"
- "Continuous subarray"
- "Cumulative"
- "Running total"
- "Sum between indices"

**When to Use:**
- ✅ Multiple range queries
- ✅ Subarray sum problems
- ✅ Need for cumulative data
- ✅ 2D matrix range queries

**Time:** O(n) preprocessing, O(1) query  
**Space:** O(n)

---

### **Binary Search**
**Trigger Words:**
- "Sorted array"
- "Find in O(log n)"
- "Rotated sorted array"
- "First/last occurrence"
- "Smallest/largest that satisfies"
- "Minimize maximum"
- "Maximize minimum"

**When to Use:**
- ✅ Data is sorted/rotated
- ✅ Search space can be divided
- ✅ Monotonic property exists
- ✅ Answer space search

**Time:** O(log n)  
**Space:** O(1)

---

### **Hash Map / Hash Set**
**Trigger Words:**
- "Count frequency"
- "Find duplicate"
- "Check existence"
- "Anagram"
- "Group by"
- "O(1) lookup"
- "Complement"

**When to Use:**
- ✅ Need fast lookups
- ✅ Frequency counting
- ✅ Detecting duplicates
- ✅ Grouping items

**Time:** O(1) average per operation  
**Space:** O(n)

---

### **Stack**
**Trigger Words:**
- "Valid parentheses"
- "Balanced"
- "Nested"
- "Most recent"
- "Evaluate expression"
- "Decode"
- "Backtrack"

**When to Use:**
- ✅ Matching/balancing problems
- ✅ Expression evaluation
- ✅ Nested structures
- ✅ Undo operations

**Time:** O(n)  
**Space:** O(n)

---

### **Monotonic Stack**
**Trigger Words:**
- "Next greater element"
- "Next smaller element"
- "Previous greater/smaller"
- "Largest rectangle"
- "Stock span"
- "Trapping water"

**When to Use:**
- ✅ Finding next/previous greater/smaller
- ✅ Histogram problems
- ✅ Range queries with monotonic property

**Time:** O(n)  
**Space:** O(n)

---

### **Heap / Priority Queue**
**Trigger Words:**
- "Top K elements"
- "Kth largest/smallest"
- "Find median"
- "Merge K sorted"
- "Priority"
- "Scheduling"

**When to Use:**
- ✅ Top K problems
- ✅ Finding Kth element
- ✅ Running median
- ✅ Task scheduling

**Time:** O(log n) insert/delete, O(1) peek  
**Space:** O(k) for top K

---

### **Tree DFS**
**Trigger Words:**
- "Binary tree"
- "Path from root to leaf"
- "All paths"
- "Validate BST"
- "Lowest common ancestor"
- "Maximum depth"
- "Serialize tree"

**When to Use:**
- ✅ Tree traversal needed
- ✅ Path problems
- ✅ Tree properties validation
- ✅ Tree transformation

**Time:** O(n)  
**Space:** O(h) where h is height

---

### **Tree BFS**
**Trigger Words:**
- "Level order"
- "Level by level"
- "Minimum depth"
- "Right side view"
- "Zigzag"
- "Cousins"

**When to Use:**
- ✅ Level-wise processing
- ✅ Shortest path in tree
- ✅ Level-specific operations

**Time:** O(n)  
**Space:** O(w) where w is max width

---

### **Graph DFS**
**Trigger Words:**
- "Connected components"
- "Number of islands"
- "All paths"
- "Detect cycle"
- "Clone graph"
- "Course schedule"
- "Reachability"

**When to Use:**
- ✅ Connectivity problems
- ✅ Cycle detection
- ✅ Path exploration
- ✅ Component counting

**Time:** O(V + E)  
**Space:** O(V)

---

### **Graph BFS**
**Trigger Words:**
- "Shortest path"
- "Minimum steps"
- "Level by level"
- "Nearest"
- "Distance K"
- "Transformation"

**When to Use:**
- ✅ Shortest path (unweighted)
- ✅ Minimum moves/steps
- ✅ Multi-source problems

**Time:** O(V + E)  
**Space:** O(V)

---

### **Topological Sort**
**Trigger Words:**
- "Prerequisites"
- "Dependencies"
- "Order of"
- "Schedule"
- "Directed graph"
- "Build order"

**When to Use:**
- ✅ Dependency resolution
- ✅ Task scheduling
- ✅ Ordering with constraints
- ✅ DAG problems

**Time:** O(V + E)  
**Space:** O(V)

---

### **Union-Find**
**Trigger Words:**
- "Connected components"
- "Disjoint sets"
- "Union"
- "Find"
- "Dynamic connectivity"
- "Provinces/networks"

**When to Use:**
- ✅ Connectivity queries
- ✅ Cycle detection (undirected)
- ✅ Grouping/clustering
- ✅ Dynamic connections

**Time:** O(α(n)) ≈ O(1) per operation  
**Space:** O(n)

---

### **Merge Intervals**
**Trigger Words:**
- "Overlapping intervals"
- "Merge"
- "Schedule"
- "Meeting rooms"
- "Calendar"
- "Time ranges"

**When to Use:**
- ✅ Interval overlapping
- ✅ Scheduling problems
- ✅ Range merging
- ✅ Calendar conflicts

**Time:** O(n log n)  
**Space:** O(n)

---

### **Backtracking**
**Trigger Words:**
- "All combinations"
- "All permutations"
- "All subsets"
- "Generate"
- "Find all solutions"
- "N-Queens"
- "Sudoku"

**When to Use:**
- ✅ Generate all possibilities
- ✅ Constraint satisfaction
- ✅ Combinatorial problems
- ✅ Puzzle solving

**Time:** Exponential (often O(2^n) or O(n!))  
**Space:** O(n) for recursion

---

### **Dynamic Programming**
**Trigger Words:**
- "Maximum/minimum"
- "Count ways"
- "Longest"
- "Shortest"
- "Optimize"
- "Can you reach"
- "Overlapping subproblems"

**When to Use:**
- ✅ Optimization problems
- ✅ Counting problems
- ✅ Overlapping subproblems
- ✅ Optimal substructure

**Sub-patterns:**
- Fibonacci: f(n) depends on f(n-1), f(n-2)
- Knapsack: Include/exclude decisions
- LCS/LIS: Sequence problems
- Matrix: Grid traversal

**Time:** Usually O(n²) or O(n×m)  
**Space:** O(n) to O(n×m)

---

## 🔍 Pattern Selection Decision Tree

```
Problem → Question Flow → Pattern

1. IS IT SORTED?
   Yes → Binary Search / Two Pointers
   No  → Continue...

2. CONTIGUOUS SEQUENCE?
   Yes → Sliding Window / Prefix Sum
   No  → Continue...

3. LINKED LIST?
   Yes → Fast & Slow Pointers / Reversal
   No  → Continue...

4. TREE/GRAPH?
   Yes → DFS / BFS / Topological Sort
   No  → Continue...

5. NEED K ELEMENTS?
   Yes → Heap / Top K Pattern
   No  → Continue...

6. OPTIMIZATION/COUNTING?
   Yes → Dynamic Programming / Greedy
   No  → Continue...

7. GENERATE ALL SOLUTIONS?
   Yes → Backtracking
   No  → Hash Map / Other patterns
```

---

## 💡 Quick Pattern Matching Guide

### By Data Structure

| Data Structure | Primary Patterns |
|----------------|------------------|
| **Array/String** | Two Pointers, Sliding Window, Binary Search, Prefix Sum |
| **Linked List** | Fast & Slow Pointers, Reversal, Two Pointers |
| **Stack/Queue** | Stack Operations, Monotonic Stack, BFS |
| **Tree** | DFS (Preorder/Inorder/Postorder), BFS, BST operations |
| **Graph** | DFS, BFS, Topological Sort, Union-Find |
| **Heap** | Top K Elements, Priority Queue, Merge K |
| **Matrix** | DFS/BFS, DP, Matrix Traversal |

### By Problem Type

| Problem Type | Primary Patterns |
|--------------|------------------|
| **Search** | Binary Search, BFS, DFS |
| **Optimization** | DP, Greedy, Binary Search on Answer |
| **Counting** | DP, Combinatorics, Hash Map |
| **Matching** | Stack, Hash Map, Two Pointers |
| **Scheduling** | Intervals, Heap, Greedy |
| **Connectivity** | Union-Find, DFS, BFS |
| **Generation** | Backtracking, DFS |

---

## 🎓 Pattern Learning Order (Beginner to Advanced)

### **Week 1-2: Foundations**
1. Two Pointers
2. Sliding Window
3. Fast & Slow Pointers
4. Prefix Sum

### **Week 3-4: Search & Hash**
5. Binary Search
6. Hash Map & Hash Set

### **Week 5-6: Linear Structures**
7. Stack & Queue
8. Monotonic Stack
9. Linked List Operations

### **Week 7-9: Trees**
10. Tree DFS
11. Tree BFS
12. BST Operations

### **Week 10-12: Advanced Structures**
13. Heap/Priority Queue
14. Graph DFS/BFS
15. Topological Sort
16. Union-Find

### **Week 13-15: Optimization**
17. Intervals
18. Greedy Algorithms
19. Dynamic Programming (Basic)

### **Week 16-18: Mastery**
20. Backtracking
21. Advanced DP
22. Bit Manipulation
23. Trie

---

## 📊 Pattern Frequency in Interviews

| Pattern | Frequency | Importance |
|---------|-----------|------------|
| Dynamic Programming | ⭐⭐⭐⭐⭐ | Very High |
| Two Pointers | ⭐⭐⭐⭐⭐ | Very High |
| Binary Search | ⭐⭐⭐⭐⭐ | Very High |
| DFS/BFS | ⭐⭐⭐⭐⭐ | Very High |
| Sliding Window | ⭐⭐⭐⭐ | High |
| Hash Map | ⭐⭐⭐⭐ | High |
| Heap | ⭐⭐⭐⭐ | High |
| Backtracking | ⭐⭐⭐ | Medium |
| Union-Find | ⭐⭐⭐ | Medium |
| Trie | ⭐⭐ | Medium-Low |
| Bit Manipulation | ⭐⭐ | Medium-Low |

---

## 🚀 Problem-Solving Checklist

Before coding:
- [ ] Identify data structures involved
- [ ] Look for trigger words
- [ ] Check if sorted/contiguous/cyclic
- [ ] Determine optimization type (time/space)
- [ ] Identify pattern(s) that fit
- [ ] Consider edge cases
- [ ] Verify time/space complexity

During coding:
- [ ] Write clean, readable code
- [ ] Add comments for complex logic
- [ ] Test with examples
- [ ] Check boundary conditions

After coding:
- [ ] Verify correctness
- [ ] Analyze time complexity
- [ ] Analyze space complexity
- [ ] Consider optimizations

---

## 📝 Common Pitfalls & Tips

### Two Pointers
❌ Forgetting to handle duplicates  
✅ Skip duplicates with while loops

### Sliding Window
❌ Not updating window state correctly  
✅ Track what enters/exits window carefully

### Binary Search
❌ Off-by-one errors  
✅ Use `left + (right - left) // 2`

### DFS/BFS
❌ Not marking visited  
✅ Always track visited nodes

### Dynamic Programming
❌ Missing base cases  
✅ Start with small examples

### Backtracking
❌ Forgetting to backtrack  
✅ Always undo choices (pop/remove)

---

## 🎯 Pattern Combination Examples

Some problems use **multiple patterns**:

1. **Sliding Window + Hash Map**
   - Longest Substring Without Repeating Characters
   - Minimum Window Substring

2. **Binary Search + Two Pointers**
   - 3Sum Closest
   - Search in Rotated Array

3. **DFS + Dynamic Programming**
   - Longest Increasing Path in Matrix
   - House Robber III

4. **BFS + Hash Map**
   - Word Ladder
   - Open the Lock

5. **Heap + Hash Map**
   - Top K Frequent Elements
   - Task Scheduler

---

## 🔥 Quick Recognition Examples

| Problem Statement Snippet | Pattern |
|---------------------------|---------|
| "Find two numbers that sum to target in **sorted** array" | Two Pointers |
| "Maximum sum of **subarray of size k**" | Sliding Window |
| "Detect **cycle** in linked list" | Fast & Slow Pointers |
| "**Range sum** query for multiple queries" | Prefix Sum |
| "Search in **rotated sorted** array" | Binary Search |
| "Count **frequency** of elements" | Hash Map |
| "**Valid parentheses**" | Stack |
| "**Next greater** element" | Monotonic Stack |
| "**Top K** largest elements" | Heap |
| "Find **all paths** in graph" | DFS |
| "**Shortest path** in unweighted graph" | BFS |
| "**Course prerequisites**" | Topological Sort |
| "Number of **connected components**" | Union-Find |
| "**Merge overlapping** intervals" | Merge Intervals |
| "**Maximum profit** with constraints" | Dynamic Programming |
| "Generate **all permutations**" | Backtracking |

---

**Remember:** 
- Pattern recognition is a skill that improves with practice
- Same problem can often be solved with different patterns
- Choose the pattern that gives best time/space complexity
- Understanding WHY a pattern works is more important than memorizing solutions

**Happy Pattern Hunting! 🎯**
