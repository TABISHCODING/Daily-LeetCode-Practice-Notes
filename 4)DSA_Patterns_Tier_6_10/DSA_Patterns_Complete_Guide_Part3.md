# Ultimate DSA Patterns Guide - Part 3
## Advanced Patterns (Tiers 6-10) & Dynamic Programming

---

# TIER 6: Heap Patterns (Week 9)

## 16. Heap/Priority Queue Pattern

### 📖 What is it?
Heap is a binary tree where parent is always greater (max-heap) or smaller (min-heap) than children. Priority Queue is typically implemented using heap, providing O(log n) insert/delete and O(1) access to min/max.

### 🎯 When to Use?
- **Top K Elements**: Finding K largest/smallest
- **Kth Element**: Kth largest/smallest
- **Median Finding**: Running median
- **Merge K Lists**: Combining sorted sequences
- **Scheduling**: Task scheduling with priorities

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Top K"
- "Kth largest/smallest"
- "Find median"
- "Merge K sorted"
- "Priority"
- "Closest K points"
- "Schedule tasks"

### 💡 Pattern Implementations

#### Variation 1: Kth Largest Element
```python
import heapq

def find_kth_largest(nums, k):
    """
    Find kth largest using min-heap of size k
    """
    # Maintain min-heap of k largest elements
    heap = nums[:k]
    heapq.heapify(heap)
    
    for num in nums[k:]:
        if num > heap[0]:
            heapq.heapreplace(heap, num)
    
    return heap[0]

# Alternative: Use max-heap
def find_kth_largest_maxheap(nums, k):
    """Using negative values to simulate max-heap"""
    heap = [-num for num in nums]
    heapq.heapify(heap)
    
    for _ in range(k - 1):
        heapq.heappop(heap)
    
    return -heap[0]

# Time: O(n log k), Space: O(k)
```

#### Variation 2: Top K Frequent Elements
```python
def top_k_frequent(nums, k):
    """
    Find k most frequent elements
    """
    from collections import Counter
    
    # Count frequencies
    count = Counter(nums)
    
    # Method 1: Using heap
    return heapq.nlargest(k, count.keys(), key=count.get)
    
    # Method 2: Manual heap approach
    heap = []
    for num, freq in count.items():
        heapq.heappush(heap, (freq, num))
        if len(heap) > k:
            heapq.heappop(heap)
    
    return [num for freq, num in heap]

# Time: O(n log k), Space: O(n)
```

#### Variation 3: Median Finder
```python
class MedianFinder:
    """
    Find median from data stream
    Uses two heaps: max-heap for smaller half, min-heap for larger half
    """
    def __init__(self):
        self.small = []  # Max-heap (use negative values)
        self.large = []  # Min-heap
    
    def addNum(self, num):
        # Add to appropriate heap
        if not self.small or num <= -self.small[0]:
            heapq.heappush(self.small, -num)
        else:
            heapq.heappush(self.large, num)
        
        # Balance heaps
        if len(self.small) > len(self.large) + 1:
            val = -heapq.heappop(self.small)
            heapq.heappush(self.large, val)
        elif len(self.large) > len(self.small):
            val = heapq.heappop(self.large)
            heapq.heappush(self.small, -val)
    
    def findMedian(self):
        if len(self.small) > len(self.large):
            return -self.small[0]
        return (-self.small[0] + self.large[0]) / 2.0

# Time: O(log n) per add, O(1) for median
# Space: O(n)
```

#### Variation 4: Merge K Sorted Lists
```python
def merge_k_sorted_lists(lists):
    """
    Merge k sorted linked lists
    """
    heap = []
    
    # Add first node from each list
    for i, lst in enumerate(lists):
        if lst:
            heapq.heappush(heap, (lst.val, i, lst))
    
    dummy = ListNode(0)
    current = dummy
    
    while heap:
        val, i, node = heapq.heappop(heap)
        current.next = node
        current = current.next
        
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))
    
    return dummy.next

# Time: O(N log k) where N = total nodes, k = lists
# Space: O(k)
```

#### Variation 5: Task Scheduler
```python
def least_interval(tasks, n):
    """
    Schedule tasks with cooldown period n
    Same task must wait n intervals
    """
    from collections import Counter
    
    # Count task frequencies
    freq = Counter(tasks)
    max_heap = [-count for count in freq.values()]
    heapq.heapify(max_heap)
    
    time = 0
    
    while max_heap:
        cycle = []
        
        # Process up to n+1 tasks
        for _ in range(n + 1):
            if max_heap:
                count = heapq.heappop(max_heap)
                if count < -1:
                    cycle.append(count + 1)
        
        # Add back to heap
        for count in cycle:
            heapq.heappush(max_heap, count)
        
        # Add time
        if max_heap:
            time += n + 1
        else:
            time += len(cycle)
    
    return time

# Time: O(n), Space: O(1) - at most 26 tasks
```

### 📝 Problem Categories & Difficulty Progression

#### Medium
1. **Kth Largest Element in an Array** (LC #215)
2. **Top K Frequent Elements** (LC #347)
3. **K Closest Points to Origin** (LC #973)
4. **Kth Smallest Element in a Sorted Matrix** (LC #378)
5. **Find K Pairs with Smallest Sums** (LC #373)
6. **Reorganize String** (LC #767)
7. **Task Scheduler** (LC #621)
8. **Sort Characters By Frequency** (LC #451)
9. **Last Stone Weight** (LC #1046)
10. **Minimum Cost to Connect Sticks** (LC #1167)

#### Hard
11. **Find Median from Data Stream** (LC #295)
12. **Merge k Sorted Lists** (LC #23)
13. **Smallest Range Covering Elements from K Lists** (LC #632)
14. **Employee Free Time** (LC #759)
15. **Sliding Window Median** (LC #480)
16. **IPO** (LC #502)

---

## 17. Top K Elements Pattern

### 📖 What is it?
Specialized pattern for finding K largest/smallest elements. Combines heap with other techniques for optimal solutions.

### 💡 Advanced Techniques

#### Quick Select for Kth Element
```python
def find_kth_largest_quickselect(nums, k):
    """
    QuickSelect algorithm - average O(n)
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

---

# TIER 7: Graph Patterns (Weeks 10-11)

## 18. Graph DFS Pattern

### 📖 What is it?
Depth-First Search explores graph by going as deep as possible before backtracking. Used for connectivity, paths, and cycles.

### 🎯 When to Use?
- **Connected Components**: Finding islands, networks
- **Cycle Detection**: Detecting loops
- **Path Finding**: All paths, specific paths
- **Topological Sort**: Dependency resolution

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Connected components"
- "Number of islands"
- "All paths"
- "Detect cycle"
- "Clone graph"
- "Course schedule"

### 💡 Pattern Implementations

#### Variation 1: Number of Islands
```python
def num_islands(grid):
    """
    Count number of islands (connected components)
    """
    if not grid:
        return 0
    
    def dfs(i, j):
        if (i < 0 or i >= len(grid) or 
            j < 0 or j >= len(grid[0]) or 
            grid[i][j] == '0'):
            return
        
        grid[i][j] = '0'  # Mark visited
        
        # Visit all 4 directions
        dfs(i + 1, j)
        dfs(i - 1, j)
        dfs(i, j + 1)
        dfs(i, j - 1)
    
    count = 0
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == '1':
                dfs(i, j)
                count += 1
    
    return count

# Time: O(m * n), Space: O(m * n) for recursion
```

#### Variation 2: Clone Graph
```python
def clone_graph(node):
    """
    Deep copy of graph using DFS
    """
    if not node:
        return None
    
    clones = {}
    
    def dfs(node):
        if node in clones:
            return clones[node]
        
        clone = Node(node.val)
        clones[node] = clone
        
        for neighbor in node.neighbors:
            clone.neighbors.append(dfs(neighbor))
        
        return clone
    
    return dfs(node)

# Time: O(V + E), Space: O(V)
```

#### Variation 3: All Paths from Source to Target
```python
def all_paths_source_target(graph):
    """
    Find all paths from node 0 to node n-1
    """
    def dfs(node, path, result):
        if node == len(graph) - 1:
            result.append(path[:])
            return
        
        for neighbor in graph[node]:
            path.append(neighbor)
            dfs(neighbor, path, result)
            path.pop()  # Backtrack
    
    result = []
    dfs(0, [0], result)
    return result

# Time: O(2^V * V), Space: O(V)
```

#### Variation 4: Detect Cycle (Undirected)
```python
def has_cycle(n, edges):
    """
    Detect cycle in undirected graph
    """
    graph = [[] for _ in range(n)]
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)
    
    visited = set()
    
    def dfs(node, parent):
        visited.add(node)
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                if dfs(neighbor, node):
                    return True
            elif neighbor != parent:
                return True  # Cycle found
        
        return False
    
    for i in range(n):
        if i not in visited:
            if dfs(i, -1):
                return True
    
    return False

# Time: O(V + E), Space: O(V)
```

### 📝 Problem Categories

#### Medium
1. **Number of Islands** (LC #200)
2. **Clone Graph** (LC #133)
3. **Pacific Atlantic Water Flow** (LC #417)
4. **Course Schedule** (LC #207)
5. **Course Schedule II** (LC #210)
6. **All Paths From Source to Target** (LC #797)
7. **Keys and Rooms** (LC #841)
8. **Surrounded Regions** (LC #130)
9. **Redundant Connection** (LC #684)

#### Hard
10. **Word Ladder II** (LC #126)
11. **Critical Connections in a Network** (LC #1192)

---

## 19. Graph BFS Pattern

### 📖 What is it?
Breadth-First Search explores graph level by level. Guarantees shortest path in unweighted graphs.

### 🎯 When to Use?
- **Shortest Path**: Minimum steps/distance
- **Level Order**: Processing by distance
- **Minimum Transformation**: Word ladder
- **Bidirectional Search**: Meet in middle

### 💡 Pattern Implementations

#### Variation 1: Shortest Path in Binary Matrix
```python
def shortest_path_binary_matrix(grid):
    """
    Find shortest path from top-left to bottom-right
    8 directions allowed
    """
    from collections import deque
    
    n = len(grid)
    if grid[0][0] == 1 or grid[n-1][n-1] == 1:
        return -1
    
    if n == 1:
        return 1
    
    queue = deque([(0, 0, 1)])  # (row, col, distance)
    grid[0][0] = 1  # Mark visited
    
    directions = [(-1,-1), (-1,0), (-1,1), (0,-1), 
                  (0,1), (1,-1), (1,0), (1,1)]
    
    while queue:
        row, col, dist = queue.popleft()
        
        for dr, dc in directions:
            r, c = row + dr, col + dc
            
            if (0 <= r < n and 0 <= c < n and grid[r][c] == 0):
                if r == n-1 and c == n-1:
                    return dist + 1
                
                queue.append((r, c, dist + 1))
                grid[r][c] = 1  # Mark visited
    
    return -1

# Time: O(n²), Space: O(n²)
```

#### Variation 2: Word Ladder
```python
def ladder_length(beginWord, endWord, wordList):
    """
    Find shortest transformation sequence
    """
    from collections import deque, defaultdict
    
    if endWord not in wordList:
        return 0
    
    # Build pattern dictionary
    word_list = set(wordList)
    patterns = defaultdict(list)
    
    for word in word_list:
        for i in range(len(word)):
            pattern = word[:i] + '*' + word[i+1:]
            patterns[pattern].append(word)
    
    # BFS
    queue = deque([(beginWord, 1)])
    visited = {beginWord}
    
    while queue:
        word, level = queue.popleft()
        
        for i in range(len(word)):
            pattern = word[:i] + '*' + word[i+1:]
            
            for next_word in patterns[pattern]:
                if next_word == endWord:
                    return level + 1
                
                if next_word not in visited:
                    visited.add(next_word)
                    queue.append((next_word, level + 1))
    
    return 0

# Time: O(M² * N) where M = word length, N = words
# Space: O(M² * N)
```

### 📝 Problem Categories

#### Medium
1. **Binary Tree Level Order Traversal** (LC #102)
2. **Rotting Oranges** (LC #994)
3. **Walls and Gates** (LC #286)
4. **01 Matrix** (LC #542)
5. **As Far from Land as Possible** (LC #1162)
6. **Shortest Path in Binary Matrix** (LC #1091)
7. **Open the Lock** (LC #752)

#### Hard
8. **Word Ladder** (LC #127)
9. **Word Ladder II** (LC #126)
10. **Minimum Knight Moves** (LC #1197)

---

## 20. Topological Sort Pattern

### 📖 What is it?
Orders vertices in Directed Acyclic Graph (DAG) such that for edge u→v, u appears before v. Used for dependency resolution, task scheduling.

### 🎯 When to Use?
- **Course Prerequisites**: Scheduling courses
- **Build Order**: Compilation dependencies
- **Task Scheduling**: Order of execution
- **Alien Dictionary**: Character ordering

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Prerequisites"
- "Dependencies"
- "Order of"
- "Schedule"
- "Directed graph"
- "Course schedule"

### 💡 Pattern Implementations

#### Method 1: Kahn's Algorithm (BFS)
```python
def findOrder(numCourses, prerequisites):
    """
    Course Schedule II - Return valid order
    """
    from collections import deque, defaultdict
    
    # Build graph and in-degree
    graph = defaultdict(list)
    in_degree = [0] * numCourses
    
    for course, prereq in prerequisites:
        graph[prereq].append(course)
        in_degree[course] += 1
    
    # Start with courses having no prerequisites
    queue = deque([i for i in range(numCourses) if in_degree[i] == 0])
    order = []
    
    while queue:
        course = queue.popleft()
        order.append(course)
        
        # Reduce in-degree of neighbors
        for neighbor in graph[course]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    
    # Check if all courses can be finished
    return order if len(order) == numCourses else []

# Time: O(V + E), Space: O(V + E)
```

#### Method 2: DFS with States
```python
def findOrder_dfs(numCourses, prerequisites):
    """
    Using DFS - Post-order gives reverse topological sort
    """
    from collections import defaultdict
    
    graph = defaultdict(list)
    for course, prereq in prerequisites:
        graph[prereq].append(course)
    
    # 0 = unvisited, 1 = visiting, 2 = visited
    state = [0] * numCourses
    order = []
    has_cycle = False
    
    def dfs(course):
        nonlocal has_cycle
        
        if state[course] == 1:  # Cycle detected
            has_cycle = True
            return
        
        if state[course] == 2:  # Already visited
            return
        
        state[course] = 1  # Mark as visiting
        
        for neighbor in graph[course]:
            dfs(neighbor)
            if has_cycle:
                return
        
        state[course] = 2  # Mark as visited
        order.append(course)
    
    for i in range(numCourses):
        if state[i] == 0:
            dfs(i)
            if has_cycle:
                return []
    
    return order[::-1]  # Reverse for topological order

# Time: O(V + E), Space: O(V + E)
```

### 📝 Problem Categories

#### Medium
1. **Course Schedule** (LC #207)
2. **Course Schedule II** (LC #210)
3. **Minimum Height Trees** (LC #310)
4. **Sequence Reconstruction** (LC #444)
5. **Sort Items by Groups Respecting Dependencies** (LC #1203)

#### Hard
6. **Alien Dictionary** (LC #269)
7. **Parallel Courses III** (LC #2050)

---

## 21. Union-Find (Disjoint Set Union) Pattern

### 📖 What is it?
Union-Find tracks disjoint sets and provides near-constant time operations for union and find. Used for connectivity problems.

### 🎯 When to Use?
- **Connected Components**: Dynamic connectivity
- **Cycle Detection**: In undirected graphs
- **Minimum Spanning Tree**: Kruskal's algorithm
- **Network Connectivity**: Social networks

### 🔍 How to Identify?
**Trigger Words/Phrases:**
- "Connected components"
- "Disjoint sets"
- "Union"
- "Find"
- "Dynamic connectivity"
- "Number of provinces"

### 💡 Pattern Implementation

```python
class UnionFind:
    """
    Union-Find with path compression and union by rank
    """
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
        self.count = n  # Number of components
    
    def find(self, x):
        """Find with path compression"""
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
    
    def union(self, x, y):
        """Union by rank"""
        root_x = self.find(x)
        root_y = self.find(y)
        
        if root_x == root_y:
            return False  # Already connected
        
        # Union by rank
        if self.rank[root_x] < self.rank[root_y]:
            self.parent[root_x] = root_y
        elif self.rank[root_x] > self.rank[root_y]:
            self.parent[root_y] = root_x
        else:
            self.parent[root_y] = root_x
            self.rank[root_x] += 1
        
        self.count -= 1
        return True
    
    def connected(self, x, y):
        """Check if x and y are connected"""
        return self.find(x) == self.find(y)
    
    def get_count(self):
        """Get number of components"""
        return self.count

# Time: O(α(n)) ≈ O(1) per operation
# Space: O(n)
```

#### Application: Number of Provinces
```python
def findCircleNum(isConnected):
    """
    Find number of provinces (connected components)
    """
    n = len(isConnected)
    uf = UnionFind(n)
    
    for i in range(n):
        for j in range(i + 1, n):
            if isConnected[i][j]:
                uf.union(i, j)
    
    return uf.get_count()

# Time: O(n²), Space: O(n)
```

#### Application: Redundant Connection
```python
def findRedundantConnection(edges):
    """
    Find edge that creates cycle in tree
    """
    n = len(edges)
    uf = UnionFind(n + 1)
    
    for u, v in edges:
        if not uf.union(u, v):
            return [u, v]  # This edge creates cycle
    
    return []

# Time: O(n), Space: O(n)
```

### 📝 Problem Categories

#### Medium
1. **Number of Provinces** (LC #547)
2. **Number of Islands** (LC #200)
3. **Graph Valid Tree** (LC #261)
4. **Number of Connected Components** (LC #323)
5. **Redundant Connection** (LC #684)
6. **Accounts Merge** (LC #721)
7. **Satisfiability of Equality Equations** (LC #990)
8. **Most Stones Removed with Same Row or Column** (LC #947)

#### Hard
9. **Redundant Connection II** (LC #685)
10. **Smallest String With Swaps** (LC #1202)
11. **Number of Islands II** (LC #305)

---

# TIER 8: Interval Patterns (Week 12)

## 22. Merge Intervals Pattern

### 📖 What is it?
Handling overlapping intervals by sorting and merging. Core technique for scheduling and range problems.

### 🎯 When to Use?
- **Overlapping Ranges**: Time, number ranges
- **Scheduling**: Meeting rooms, appointments
- **Calendar Problems**: Free/busy time
- **Range Merging**: Combining intervals

### 💡 Pattern Implementation

```python
def merge_intervals(intervals):
    """
    Merge overlapping intervals
    """
    if not intervals:
        return []
    
    # Sort by start time
    intervals.sort(key=lambda x: x[0])
    
    merged = [intervals[0]]
    
    for current in intervals[1:]:
        last = merged[-1]
        
        if current[0] <= last[1]:  # Overlapping
            # Merge
            last[1] = max(last[1], current[1])
        else:
            # Non-overlapping
            merged.append(current)
    
    return merged

# Time: O(n log n), Space: O(n)
```

### 📝 Problem Categories

#### Easy
1. **Meeting Rooms** (LC #252)

#### Medium
2. **Merge Intervals** (LC #56)
3. **Insert Interval** (LC #57)
4. **Non-overlapping Intervals** (LC #435)
5. **Meeting Rooms II** (LC #253)
6. **Minimum Number of Arrows** (LC #452)
7. **Interval List Intersections** (LC #986)
8. **Car Pooling** (LC #1094)
9. **My Calendar I** (LC #729)

#### Hard
10. **Employee Free Time** (LC #759)
11. **My Calendar III** (LC #732)

---

# TIER 9: Matrix Patterns (Week 13)

## 24. Matrix Traversal Pattern

### 📖 What is it?
Systematic exploration of 2D grids using DFS/BFS. Common in grid-based problems.

### 💡 Key Techniques

```python
def spiral_order(matrix):
    """
    Traverse matrix in spiral order
    """
    if not matrix:
        return []
    
    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1
    
    while top <= bottom and left <= right:
        # Traverse right
        for col in range(left, right + 1):
            result.append(matrix[top][col])
        top += 1
        
        # Traverse down
        for row in range(top, bottom + 1):
            result.append(matrix[row][right])
        right -= 1
        
        if top <= bottom:
            # Traverse left
            for col in range(right, left - 1, -1):
                result.append(matrix[bottom][col])
            bottom -= 1
        
        if left <= right:
            # Traverse up
            for row in range(bottom, top - 1, -1):
                result.append(matrix[row][left])
            left += 1
    
    return result

# Time: O(m * n), Space: O(1)
```

### 📝 Problem Categories

#### Easy
1. **Flood Fill** (LC #733)
2. **Island Perimeter** (LC #463)

#### Medium
3. **Number of Islands** (LC #200)
4. **Surrounded Regions** (LC #130)
5. **Spiral Matrix** (LC #54)
6. **Rotate Image** (LC #48)
7. **Set Matrix Zeroes** (LC #73)
8. **Word Search** (LC #79)
9. **Pacific Atlantic Water Flow** (LC #417)

---

# TIER 10: Advanced Patterns (Weeks 14-18)

## 26. Backtracking Pattern

### 📖 What is it?
Explores all possibilities by building solutions incrementally and abandoning paths that don't work (backtracking).

### 🎯 When to Use?
- **Combinations**: All possible combinations
- **Permutations**: All arrangements
- **Subsets**: Powerset generation
- **Puzzles**: Sudoku, N-Queens
- **Path Finding**: All possible paths

### 💡 Pattern Implementations

#### Template
```python
def backtrack_template(candidates, target):
    """
    General backtracking template
    """
    result = []
    
    def backtrack(start, path, remaining):
        # Base case
        if remaining == 0:
            result.append(path[:])
            return
        
        # Pruning
        if remaining < 0:
            return
        
        # Try all possibilities
        for i in range(start, len(candidates)):
            # Make choice
            path.append(candidates[i])
            
            # Recurse
            backtrack(i, path, remaining - candidates[i])
            
            # Undo choice (backtrack)
            path.pop()
    
    backtrack(0, [], target)
    return result
```

### 📝 Problem Categories

#### Medium
1. **Subsets** (LC #78)
2. **Subsets II** (LC #90)
3. **Permutations** (LC #46)
4. **Permutations II** (LC #47)
5. **Combinations** (LC #77)
6. **Combination Sum** (LC #39)
7. **Combination Sum II** (LC #40)
8. **Palindrome Partitioning** (LC #131)
9. **Letter Combinations of a Phone Number** (LC #17)
10. **Generate Parentheses** (LC #22)

#### Hard
11. **N-Queens** (LC #51)
12. **Sudoku Solver** (LC #37)
13. **Word Search II** (LC #212)

---

## 27. Dynamic Programming Pattern

### 📖 What is it?
Solves problems by breaking into overlapping subproblems, storing solutions to avoid recomputation.

### 🎯 Main Sub-patterns

1. **Fibonacci Pattern**: f(n) = f(n-1) + f(n-2)
2. **0/1 Knapsack**: Include or exclude items
3. **Unbounded Knapsack**: Unlimited items
4. **LCS/LIS**: Longest Common/Increasing Subsequence
5. **Matrix Chain**: Optimal multiplication order
6. **DP on Strings**: Edit distance, matching
7. **DP on Trees**: Max path sum
8. **State Machine DP**: Stock trading
9. **Digit DP**: Number problems

### 💡 Core Patterns

#### Pattern 1: Fibonacci (Linear DP)
```python
def climb_stairs(n):
    """
    Climbing Stairs - Fibonacci pattern
    """
    if n <= 2:
        return n
    
    # dp[i] = ways to reach step i
    prev2, prev1 = 1, 2
    
    for i in range(3, n + 1):
        current = prev1 + prev2
        prev2, prev1 = prev1, current
    
    return prev1

# Time: O(n), Space: O(1)
```

#### Pattern 2: 0/1 Knapsack
```python
def knapsack_01(weights, values, capacity):
    """
    0/1 Knapsack - each item once
    """
    n = len(weights)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]
    
    for i in range(1, n + 1):
        for w in range(capacity + 1):
            if weights[i-1] <= w:
                # Max of include or exclude
                dp[i][w] = max(
                    values[i-1] + dp[i-1][w - weights[i-1]],  # Include
                    dp[i-1][w]  # Exclude
                )
            else:
                dp[i][w] = dp[i-1][w]
    
    return dp[n][capacity]

# Time: O(n * capacity), Space: O(n * capacity)
```

#### Pattern 3: LCS (String DP)
```python
def longest_common_subsequence(text1, text2):
    """
    Find length of LCS
    """
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[m][n]

# Time: O(m * n), Space: O(m * n)
```

### 📝 Problem Categories by Sub-pattern

#### Fibonacci Pattern
1. **Climbing Stairs** (LC #70)
2. **House Robber** (LC #198)
3. **House Robber II** (LC #213)
4. **Min Cost Climbing Stairs** (LC #746)

#### Knapsack Pattern
5. **Partition Equal Subset Sum** (LC #416)
6. **Target Sum** (LC #494)
7. **Coin Change** (LC #322)
8. **Coin Change 2** (LC #518)

#### LCS/LIS Pattern
9. **Longest Common Subsequence** (LC #1143)
10. **Longest Increasing Subsequence** (LC #300)
11. **Edit Distance** (LC #72)
12. **Distinct Subsequences** (LC #115)

#### Matrix DP
13. **Unique Paths** (LC #62)
14. **Unique Paths II** (LC #63)
15. **Minimum Path Sum** (LC #64)
16. **Longest Increasing Path in Matrix** (LC #329)

#### State Machine DP
17. **Best Time to Buy and Sell Stock** (LC #121)
18. **Best Time to Buy and Sell Stock II** (LC #122)
19. **Best Time to Buy and Sell Stock with Cooldown** (LC #309)
20. **Best Time to Buy and Sell Stock IV** (LC #188)

---

## 28. Greedy Algorithms Pattern

### 📖 What is it?
Makes locally optimal choice at each step, hoping to find global optimum. Works when local optimal leads to global optimal.

### 🎯 When to Use?
- **Scheduling**: Task/job scheduling
- **Interval Problems**: Meeting rooms
- **Optimization**: Minimum/maximum problems
- **Sorting Based**: Often requires sorting first

### 💡 Key Problems

#### Jump Game
```python
def can_jump(nums):
    """
    Can reach last index
    Greedy: Track farthest reachable
    """
    max_reach = 0
    
    for i in range(len(nums)):
        if i > max_reach:
            return False
        max_reach = max(max_reach, i + nums[i])
        if max_reach >= len(nums) - 1:
            return True
    
    return True

# Time: O(n), Space: O(1)
```

### 📝 Problem Categories

#### Easy
1. **Assign Cookies** (LC #455)
2. **Lemonade Change** (LC #860)

#### Medium
3. **Jump Game** (LC #55)
4. **Jump Game II** (LC #45)
5. **Gas Station** (LC #134)
6. **Task Scheduler** (LC #621)
7. **Partition Labels** (LC #763)
8. **Non-overlapping Intervals** (LC #435)

---

## 29. Bit Manipulation Pattern

### 📖 What is it?
Direct manipulation of bits for efficient operations.

### 💡 Key Operations

```python
# Basic operations
n & (n-1)  # Remove rightmost set bit
n & -n     # Isolate rightmost set bit
n | (1 << i)  # Set ith bit
n & ~(1 << i)  # Clear ith bit
n ^ (1 << i)  # Toggle ith bit
```

### 📝 Problem Categories

#### Easy
1. **Single Number** (LC #136)
2. **Number of 1 Bits** (LC #191)
3. **Counting Bits** (LC #338)

#### Medium
4. **Single Number II** (LC #137)
5. **Single Number III** (LC #260)
6. **Subsets** (LC #78)
7. **Maximum XOR of Two Numbers** (LC #421)

---

## 30. Trie (Prefix Tree) Pattern

### 📖 What is it?
Tree structure for storing strings, enabling efficient prefix searches.

### 💡 Implementation

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end
    
    def startsWith(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
```

### 📝 Problem Categories

#### Medium
1. **Implement Trie** (LC #208)
2. **Design Add and Search Words** (LC #211)
3. **Replace Words** (LC #648)
4. **Longest Word in Dictionary** (LC #720)

#### Hard
5. **Word Search II** (LC #212)
6. **Concatenated Words** (LC #472)
7. **Palindrome Pairs** (LC #336)

---

# 🎯 Complete Learning Roadmap Summary

## Week-by-Week Plan

**Weeks 1-2**: Two Pointers, Sliding Window, Fast & Slow Pointers, Prefix Sum
**Weeks 3-4**: Binary Search, Hash Map, Sorting
**Week 5**: Stack, Monotonic Stack, Queue
**Week 6**: Linked List Operations
**Weeks 7-8**: Tree DFS, Tree BFS, BST
**Week 9**: Heap, Priority Queue
**Weeks 10-11**: Graph DFS, Graph BFS, Topological Sort, Union-Find
**Week 12**: Intervals
**Week 13**: Matrix Traversal
**Weeks 14-18**: Backtracking, Dynamic Programming, Greedy, Bit Manipulation, Trie

---

**Total Patterns Covered**: 30
**Total Problems Referenced**: 300+
**Estimated Completion Time**: 18 weeks (4-5 months)

Good luck with your coding interview preparation! 🚀