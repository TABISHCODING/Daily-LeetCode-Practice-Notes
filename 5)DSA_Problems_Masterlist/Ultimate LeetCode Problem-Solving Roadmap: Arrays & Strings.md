# 🚀 Ultimate LeetCode Problem-Solving Roadmap: Arrays & Strings

> **A comprehensive guide to mastering array and string problems with curated LeetCode questions, pattern recognition, and learning order**

---

## 📚 Table of Contents
1. [Array Problems Roadmap](#array-problems-roadmap)
2. [String Problems Roadmap](#string-problems-roadmap)
3. [Learning Strategy](#learning-strategy)
4. [Pattern Recognition Guide](#pattern-recognition-guide)

---

# 🔷 ARRAY PROBLEMS ROADMAP

---

## 🎯 Learning Path Overview

```
Basics → Sorting → Two Pointer → Sliding Window → Prefix Sum → 
Hashing → Binary Search → DP → Advanced Patterns
```

---

## 1️⃣ **Basic Array Concepts**

### 🎓 Prerequisites
- Array operations (access, insert, delete)
- Index handling and boundaries
- Traversal techniques
- Time/Space complexity basics

### 📝 Curated Problems

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 1 | Running Sum of 1d Array | Easy | [LeetCode 1480](https://leetcode.com/problems/running-sum-of-1d-array/) | `basic iteration`, `cumulative sum` |
| 2 | Richest Customer Wealth | Easy | [LeetCode 1672](https://leetcode.com/problems/richest-customer-wealth/) | `2D array`, `row sum`, `max value` |
| 3 | Shuffle the Array | Easy | [LeetCode 1470](https://leetcode.com/problems/shuffle-the-array/) | `index manipulation`, `array construction` |
| 4 | Kids With Greatest Number of Candies | Easy | [LeetCode 1431](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/) | `find max`, `comparison` |
| 5 | Number of Good Pairs | Easy | [LeetCode 1512](https://leetcode.com/problems/number-of-good-pairs/) | `nested loops`, `counting pairs` |

**🔑 Key Tricks:**
- Master `0-based indexing` and boundary checks
- Understand `in-place` vs `extra space` operations
- Practice calculating `time complexity` for nested loops

---

## 2️⃣ **Sorting Algorithms**

### 🎓 Core Concepts
- Bubble Sort, Selection Sort (O(n²))
- Merge Sort, Quick Sort (O(n log n))
- Counting Sort, Bucket Sort (special cases)
- Built-in sort usage and customization

### 📝 Curated Problems

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 6 | Sort Colors | Medium | [LeetCode 75](https://leetcode.com/problems/sort-colors/) | `Dutch National Flag`, `three-way partition`, `one-pass` |
| 7 | Sort an Array | Medium | [LeetCode 912](https://leetcode.com/problems/sort-an-array/) | `merge sort`, `quick sort`, `implementation` |
| 8 | Squares of a Sorted Array | Easy | [LeetCode 977](https://leetcode.com/problems/squares-of-a-sorted-array/) | `two pointer`, `merge technique`, `already sorted` |
| 9 | Merge Sorted Array | Easy | [LeetCode 88](https://leetcode.com/problems/merge-sorted-array/) | `merge from end`, `in-place`, `two pointers` |
| 10 | Largest Number | Medium | [LeetCode 179](https://leetcode.com/problems/largest-number/) | `custom comparator`, `string sort`, `greedy` |

**🔑 Key Tricks:**
- Recognize when input is **already sorted** or **partially sorted**
- Use **built-in sort** for simplicity unless asked to implement
- **Sort + two pointer** is a powerful combination

---

## 3️⃣ **Two Pointer Pattern** ⭐

### 🎓 When to Use
- **Keywords:** "sorted array", "pair", "triplet", "palindrome", "remove duplicates"
- **Recognition:** Need to compare elements from different positions

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 11 | Two Sum II (Sorted) | Medium | [LeetCode 167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | `opposite direction`, `sum comparison`, `sorted input` |
| 12 | Remove Duplicates from Sorted Array | Easy | [LeetCode 26](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) | `slow-fast pointer`, `in-place`, `unique elements` |
| 13 | Container With Most Water | Medium | [LeetCode 11](https://leetcode.com/problems/container-with-most-water/) | `greedy`, `area calculation`, `move shorter side` |
| 14 | 3Sum | Medium | [LeetCode 15](https://leetcode.com/problems/3sum/) | `sort first`, `skip duplicates`, `two pointer in loop` |
| 15 | 3Sum Closest | Medium | [LeetCode 16](https://leetcode.com/problems/3sum-closest/) | `track minimum diff`, `similar to 3Sum` |
| 16 | Trapping Rain Water | Hard | [LeetCode 42](https://leetcode.com/problems/trapping-rain-water/) | `two pointer`, `max left/right`, `water level` |
| 17 | Move Zeroes | Easy | [LeetCode 283](https://leetcode.com/problems/move-zeroes/) | `slow-fast pointer`, `in-place swap`, `maintain order` |
| 18 | Remove Element | Easy | [LeetCode 27](https://leetcode.com/problems/remove-element/) | `slow-fast pointer`, `overwrite` |

**🔑 Key Tricks:**
- **Opposite direction:** Start from both ends (`left=0, right=n-1`)
- **Same direction:** Fast pointer explores, slow pointer builds result
- **Skip duplicates:** Use `while` loops to skip repeated values
- **Sort first** if array is unsorted and problem allows

---

## 4️⃣ **Sliding Window Pattern** ⭐⭐

### 🎓 When to Use
- **Keywords:** "subarray", "substring", "consecutive", "window of size k", "maximum/minimum"
- **Recognition:** Finding optimal subarray with constraints

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 19 | Maximum Average Subarray I | Easy | [LeetCode 643](https://leetcode.com/problems/maximum-average-subarray-i/) | `fixed window`, `slide and update`, `sum tracking` |
| 20 | Minimum Size Subarray Sum | Medium | [LeetCode 209](https://leetcode.com/problems/minimum-size-subarray-sum/) | `variable window`, `shrink when valid`, `expand right` |
| 21 | Longest Subarray of 1s After Deleting One | Medium | [LeetCode 1493](https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/) | `count zeros`, `at most k technique` |
| 22 | Max Consecutive Ones III | Medium | [LeetCode 1004](https://leetcode.com/problems/max-consecutive-ones-iii/) | `flip at most k zeros`, `shrink when invalid` |
| 23 | Fruit Into Baskets | Medium | [LeetCode 904](https://leetcode.com/problems/fruit-into-baskets/) | `at most 2 distinct`, `hashmap`, `variable window` |
| 24 | Permutation in String | Medium | [LeetCode 567](https://leetcode.com/problems/permutation-in-string/) | `fixed window`, `frequency match`, `anagram` |
| 25 | Find All Anagrams in String | Medium | [LeetCode 438](https://leetcode.com/problems/find-all-anagrams-in-a-string/) | `sliding + hashmap`, `frequency count` |

**🔑 Key Tricks:**
- **Fixed window:** Slide by `add right, remove left`
- **Variable window:** Expand right until invalid, shrink left until valid
- Use **hashmap** for frequency tracking
- Template: `while (right < n) { expand; while (invalid) shrink; update answer; }`

---

## 5️⃣ **Prefix Sum / Cumulative Sum** ⭐

### 🎓 When to Use
- **Keywords:** "subarray sum", "range query", "sum equals k", "cumulative"
- **Recognition:** Need multiple range sums efficiently

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 26 | Running Sum of 1d Array | Easy | [LeetCode 1480](https://leetcode.com/problems/running-sum-of-1d-array/) | `build prefix array`, `prefix[i] = prefix[i-1] + arr[i]` |
| 27 | Range Sum Query - Immutable | Easy | [LeetCode 303](https://leetcode.com/problems/range-sum-query-immutable/) | `precompute prefix`, `sum = prefix[j] - prefix[i-1]` |
| 28 | Subarray Sum Equals K | Medium | [LeetCode 560](https://leetcode.com/problems/subarray-sum-equals-k/) | `prefix sum + hashmap`, `count technique`, `cumsum - k` |
| 29 | Continuous Subarray Sum | Medium | [LeetCode 523](https://leetcode.com/problems/continuous-subarray-sum/) | `prefix sum mod k`, `hashmap of remainders` |
| 30 | Product of Array Except Self | Medium | [LeetCode 238](https://leetcode.com/problems/product-of-array-except-self/) | `prefix product + suffix product`, `no division` |
| 31 | Range Sum Query 2D | Medium | [LeetCode 304](https://leetcode.com/problems/range-sum-query-2d-immutable/) | `2D prefix sum`, `inclusion-exclusion` |

**🔑 Key Tricks:**
- **Build prefix:** `prefix[i] = prefix[i-1] + arr[i]`
- **Range sum:** `sum(i, j) = prefix[j] - prefix[i-1]`
- **Subarray with sum k:** Use `hashmap` to store `prefix_sum → count`
- **2D prefix:** `prefix[i][j] = prefix[i-1][j] + prefix[i][j-1] - prefix[i-1][j-1] + matrix[i][j]`

---

## 6️⃣ **Hashing / Frequency Count** ⭐⭐

### 🎓 When to Use
- **Keywords:** "pair", "duplicate", "frequency", "contains", "unique"
- **Recognition:** Need fast lookups or counting

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 32 | Two Sum | Easy | [LeetCode 1](https://leetcode.com/problems/two-sum/) | `hashmap`, `complement = target - num`, `one pass` |
| 33 | Contains Duplicate | Easy | [LeetCode 217](https://leetcode.com/problems/contains-duplicate/) | `hashset`, `check existence` |
| 34 | Contains Duplicate II | Easy | [LeetCode 219](https://leetcode.com/problems/contains-duplicate-ii/) | `hashmap of indices`, `check distance` |
| 35 | Majority Element | Easy | [LeetCode 169](https://leetcode.com/problems/majority-element/) | `Boyer-Moore voting`, `hashmap count`, `appears > n/2` |
| 36 | Longest Consecutive Sequence | Medium | [LeetCode 128](https://leetcode.com/problems/longest-consecutive-sequence/) | `hashset`, `start of sequence`, `O(n) time` |
| 37 | Top K Frequent Elements | Medium | [LeetCode 347](https://leetcode.com/problems/top-k-frequent-elements/) | `hashmap + bucket sort`, `heap alternative` |
| 38 | Group Anagrams | Medium | [LeetCode 49](https://leetcode.com/problems/group-anagrams/) | `sorted string as key`, `hashmap grouping` |

**🔑 Key Tricks:**
- **Two Sum pattern:** Store `complement` in hashmap as you iterate
- **Frequency:** Use `Counter` or hashmap `{element: count}`
- **Index tracking:** Store `{element: index}` for position queries
- **Set for existence:** Use `set` when only checking presence

---

## 7️⃣ **Binary Search on Arrays** ⭐

### 🎓 When to Use
- **Keywords:** "sorted", "search", "find first/last", "rotated", "peak", "minimum"
- **Recognition:** Monotonic property exists (sorted or semi-sorted)

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 39 | Binary Search | Easy | [LeetCode 704](https://leetcode.com/problems/binary-search/) | `standard template`, `left <= right`, `mid = (left+right)//2` |
| 40 | First Bad Version | Easy | [LeetCode 278](https://leetcode.com/problems/first-bad-version/) | `find first`, `move right = mid - 1` |
| 41 | Search Insert Position | Easy | [LeetCode 35](https://leetcode.com/problems/search-insert-position/) | `return left`, `insertion point` |
| 42 | Find First and Last Position | Medium | [LeetCode 34](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) | `binary search twice`, `left bound + right bound` |
| 43 | Search in Rotated Sorted Array | Medium | [LeetCode 33](https://leetcode.com/problems/search-in-rotated-sorted-array/) | `identify sorted half`, `check which side target is` |
| 44 | Find Minimum in Rotated Array | Medium | [LeetCode 153](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) | `compare with right`, `find inflection point` |
| 45 | Find Peak Element | Medium | [LeetCode 162](https://leetcode.com/problems/find-peak-element/) | `compare mid with mid+1`, `go to rising side` |
| 46 | Koko Eating Bananas | Medium | [LeetCode 875](https://leetcode.com/problems/koko-eating-bananas/) | `binary search on answer`, `check feasibility` |

**🔑 Key Tricks:**
- **Standard template:** `while left <= right: mid = (left+right)//2`
- **Find first occurrence:** Move `right = mid - 1` when found
- **Find last occurrence:** Move `left = mid + 1` when found
- **Search on answer:** Binary search on possible answer range, check feasibility
- **Rotated array:** Find which half is sorted, decide which side to search

---

## 8️⃣ **Dynamic Programming on Arrays** ⭐⭐⭐

### 🎓 When to Use
- **Keywords:** "maximum", "minimum", "count ways", "subsequence", "optimization"
- **Recognition:** Need to make optimal choices, overlapping subproblems

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 47 | Climbing Stairs | Easy | [LeetCode 70](https://leetcode.com/problems/climbing-stairs/) | `fibonacci`, `dp[i] = dp[i-1] + dp[i-2]` |
| 48 | Maximum Subarray (Kadane's) | Medium | [LeetCode 53](https://leetcode.com/problems/maximum-subarray/) | `Kadane's algorithm`, `local max vs global max` |
| 49 | House Robber | Medium | [LeetCode 198](https://leetcode.com/problems/house-robber/) | `rob or skip`, `dp[i] = max(dp[i-1], dp[i-2]+nums[i])` |
| 50 | Best Time to Buy and Sell Stock | Easy | [LeetCode 121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | `track min price`, `update max profit` |
| 51 | Longest Increasing Subsequence | Medium | [LeetCode 300](https://leetcode.com/problems/longest-increasing-subsequence/) | `dp O(n²)`, `binary search O(n log n)`, `patience sort` |
| 52 | Maximum Product Subarray | Medium | [LeetCode 152](https://leetcode.com/problems/maximum-product-subarray/) | `track max and min`, `negatives flip signs` |
| 53 | Coin Change | Medium | [LeetCode 322](https://leetcode.com/problems/coin-change/) | `unbounded knapsack`, `dp[amount] = min coins` |
| 54 | Jump Game | Medium | [LeetCode 55](https://leetcode.com/problems/jump-game/) | `greedy or dp`, `track max reachable` |
| 55 | Jump Game II | Medium | [LeetCode 45](https://leetcode.com/problems/jump-game-ii/) | `BFS-like`, `track current and next boundary` |

**🔑 Key Tricks:**
- **Kadane's Algorithm:** For maximum subarray sum
- **State definition:** What does `dp[i]` represent?
- **Transition:** How to compute `dp[i]` from previous states?
- **Space optimization:** Can reduce 2D DP to 1D, or use O(1) space
- **Subsequence vs Subarray:** Subsequence can skip elements, subarray must be consecutive

---

## 9️⃣ **Merge / Partition Patterns**

### 🎓 When to Use
- **Keywords:** "intervals", "merge", "rearrange", "group", "partition"
- **Recognition:** Need to combine or separate based on conditions

### 📝 Curated Problems

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 56 | Merge Intervals | Medium | [LeetCode 56](https://leetcode.com/problems/merge-intervals/) | `sort by start`, `merge overlapping`, `compare end times` |
| 57 | Insert Interval | Medium | [LeetCode 57](https://leetcode.com/problems/insert-interval/) | `three parts`, `before, merge, after` |
| 58 | Non-overlapping Intervals | Medium | [LeetCode 435](https://leetcode.com/problems/non-overlapping-intervals/) | `greedy`, `sort by end`, `count removals` |
| 59 | Meeting Rooms | Easy | [LeetCode 252](https://leetcode.com/problems/meeting-rooms/) | `sort`, `check overlap` |
| 60 | Meeting Rooms II | Medium | [LeetCode 253](https://leetcode.com/problems/meeting-rooms-ii/) | `min heap`, `start/end times separate`, `sweep line` |
| 61 | Sort Colors | Medium | [LeetCode 75](https://leetcode.com/problems/sort-colors/) | `Dutch flag`, `three-way partition` |

**🔑 Key Tricks:**
- **Intervals:** Always **sort by start time** first
- **Merge condition:** `current.start <= previous.end`
- **Three-way partition:** Use two pointers (low, high) and iterate with mid
- **Sweep line:** Process start and end events separately

---

## 🔟 **Special Array Tricks & Advanced Patterns**

### 📝 Curated Problems

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 62 | Rotate Array | Medium | [LeetCode 189](https://leetcode.com/problems/rotate-array/) | `reverse technique`, `three reverses`, `O(1) space` |
| 63 | Next Permutation | Medium | [LeetCode 31](https://leetcode.com/problems/next-permutation/) | `find pivot`, `swap`, `reverse suffix` |
| 64 | Next Greater Element I | Easy | [LeetCode 496](https://leetcode.com/problems/next-greater-element-i/) | `monotonic stack`, `decreasing stack`, `hashmap` |
| 65 | Daily Temperatures | Medium | [LeetCode 739](https://leetcode.com/problems/daily-temperatures/) | `monotonic stack`, `store indices` |
| 66 | Largest Rectangle in Histogram | Hard | [LeetCode 84](https://leetcode.com/problems/largest-rectangle-in-histogram/) | `monotonic stack`, `extend left/right` |
| 67 | Sliding Window Maximum | Hard | [LeetCode 239](https://leetcode.com/problems/sliding-window-maximum/) | `deque`, `monotonic decreasing`, `store indices` |
| 68 | Median of Two Sorted Arrays | Hard | [LeetCode 4](https://leetcode.com/problems/median-of-two-sorted-arrays/) | `binary search`, `partition`, `O(log(min(m,n)))` |

**🔑 Key Tricks:**
- **Rotate array:** Three reverses: `reverse(0,n) → reverse(0,k) → reverse(k,n)`
- **Monotonic stack:** For "next greater/smaller" problems
- **Deque:** For sliding window maximum/minimum
- **Binary search on two arrays:** Partition both arrays to find median

---

# 🔶 STRING PROBLEMS ROADMAP

---

## 🎯 Learning Path Overview

```
Basics → Two Pointer → Hashing → Sliding Window → Prefix/Suffix → 
String Matching → DP → Stack → Advanced Patterns
```

---

## 1️⃣ **Basic String Concepts**

### 🎓 Prerequisites
- String immutability
- Common methods (split, join, replace, strip)
- Character operations (isalnum, isdigit, lower, upper)
- Substring extraction
- Index handling (positive and negative)

### 📝 Curated Problems

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 69 | Reverse String | Easy | [LeetCode 344](https://leetcode.com/problems/reverse-string/) | `two pointer`, `swap in-place` |
| 70 | Reverse Words in a String | Medium | [LeetCode 151](https://leetcode.com/problems/reverse-words-in-a-string/) | `split`, `reverse`, `join`, `strip spaces` |
| 71 | Length of Last Word | Easy | [LeetCode 58](https://leetcode.com/problems/length-of-last-word/) | `strip`, `split`, `last element` |
| 72 | To Lower Case | Easy | [LeetCode 709](https://leetcode.com/problems/to-lower-case/) | `ASCII manipulation`, `ord/chr` |
| 73 | Defanging an IP Address | Easy | [LeetCode 1108](https://leetcode.com/problems/defanging-an-ip-address/) | `replace method` |

**🔑 Key Tricks:**
- Strings are **immutable** in Python (create new string for modifications)
- Use **list** for character-by-character operations, then `''.join()`
- Master **slicing**: `s[start:end:step]`, `s[::-1]` for reverse

---

## 2️⃣ **Two Pointer Pattern (Strings)** ⭐

### 🎓 When to Use
- **Keywords:** "palindrome", "reverse", "vowels", "matching brackets"
- **Recognition:** Need to compare/match characters from different positions

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 74 | Valid Palindrome | Easy | [LeetCode 125](https://leetcode.com/problems/valid-palindrome/) | `two pointer`, `skip non-alphanumeric`, `case-insensitive` |
| 75 | Valid Palindrome II | Easy | [LeetCode 680](https://leetcode.com/problems/valid-palindrome-ii/) | `delete one char`, `check both options` |
| 76 | Reverse Vowels of a String | Easy | [LeetCode 345](https://leetcode.com/problems/reverse-vowels-of-a-string/) | `two pointer`, `swap vowels`, `set lookup` |
| 77 | Reverse String II | Easy | [LeetCode 541](https://leetcode.com/problems/reverse-string-ii/) | `reverse every 2k chars`, `slicing` |
| 78 | Is Subsequence | Easy | [LeetCode 392](https://leetcode.com/problems/is-subsequence/) | `two pointer`, `match characters`, `greedy` |
| 79 | Long Pressed Name | Easy | [LeetCode 925](https://leetcode.com/problems/long-pressed-name/) | `two pointer`, `count repetitions` |

**🔑 Key Tricks:**
- **Palindrome check:** Left and right pointers move inward
- **Skip unwanted chars:** Use `while` to skip non-alphanumeric
- **Case-insensitive:** Convert to lower/upper before comparison
- **Subsequence:** Fast pointer on main string, slow on subsequence

---

## 3️⃣ **Hashing / Frequency Count (Strings)** ⭐⭐

### 🎓 When to Use
- **Keywords:** "anagram", "character count", "frequency", "unique characters"
- **Recognition:** Need to count or compare character frequencies

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 80 | Valid Anagram | Easy | [LeetCode 242](https://leetcode.com/problems/valid-anagram/) | `sort and compare`, `frequency count`, `Counter` |
| 81 | Group Anagrams | Medium | [LeetCode 49](https://leetcode.com/problems/group-anagrams/) | `sorted string as key`, `hashmap of lists` |
| 82 | First Unique Character | Easy | [LeetCode 387](https://leetcode.com/problems/first-unique-character-in-a-string/) | `frequency map`, `find first count=1` |
| 83 | Ransom Note | Easy | [LeetCode 383](https://leetcode.com/problems/ransom-note/) | `character count`, `check availability` |
| 84 | Longest Substring Without Repeating | Medium | [LeetCode 3](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | `sliding window + hashmap`, `track last seen index` |
| 85 | Find All Anagrams in String | Medium | [LeetCode 438](https://leetcode.com/problems/find-all-anagrams-in-a-string/) | `sliding window`, `frequency match`, `fixed window` |
| 86 | Custom Sort String | Medium | [LeetCode 791](https://leetcode.com/problems/custom-sort-string/) | `frequency count`, `custom order` |

**🔑 Key Tricks:**
- **Anagram check:** Sort both strings OR compare frequency maps
- **Frequency array:** Use `[0]*26` for lowercase letters (fast)
- **Python Counter:** `from collections import Counter`
- **Sliding window + hashmap:** For substring problems with character constraints

---

## 4️⃣ **Sliding Window Pattern (Strings)** ⭐⭐⭐

### 🎓 When to Use
- **Keywords:** "substring", "longest", "shortest", "contains all", "at most K"
- **Recognition:** Finding optimal substring with constraints

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 87 | Longest Substring Without Repeating | Medium | [LeetCode 3](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | `variable window`, `hashmap last index`, `update start` |
| 88 | Minimum Window Substring | Hard | [LeetCode 76](https://leetcode.com/problems/minimum-window-substring/) | `two hashmap`, `expand/shrink`, `match count` |
| 89 | Longest Substring with At Most K Distinct | Medium | [LeetCode 340](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) | `hashmap size <= k`, `shrink when invalid` |
| 90 | Longest Repeating Character Replacement | Medium | [LeetCode 424](https://leetcode.com/problems/longest-repeating-character-replacement/) | `max frequency + k flips`, `window size validation` |
| 91 | Permutation in String | Medium | [LeetCode 567](https://leetcode.com/problems/permutation-in-string/) | `fixed window size`, `frequency match`, `anagram` |
| 92 | Substring with Concatenation of All Words | Hard | [LeetCode 30](https://leetcode.com/problems/substring-with-concatenation-of-all-words/) | `word-level sliding window`, `hashmap of words` |

**🔑 Key Tricks:**
- **Template:** `expand right → shrink left when invalid → update answer`
- **Hashmap for frequency:** Track character counts in current window
- **Distinct characters:** Use `len(hashmap)` to track unique count
- **Fixed vs variable window:** Fixed uses `if`, variable uses `while`
- **Minimum window:** Expand first to find valid, then shrink to minimize

---

## 5️⃣ **Prefix / Suffix Patterns**

### 🎓 When to Use
- **Keywords:** "common prefix", "suffix", "cumulative", "bitmasking for substrings"
- **Recognition:** Need to track cumulative properties

### 📝 Curated Problems

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 93 | Longest Common Prefix | Easy | [LeetCode 14](https://leetcode.com/problems/longest-common-prefix/) | `vertical scan`, `stop at first mismatch` |
| 94 | Implement strStr() | Easy | [LeetCode 28](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/) | `string matching`, `sliding window`, `KMP` |
| 95 | Number of Matching Subsequences | Medium | [LeetCode 792](https://leetcode.com/problems/number-of-matching-subsequences/) | `bucket by first char`, `advance pointers` |

**🔑 Key Tricks:**
- **Common prefix:** Compare characters at same position across all strings
- **Trie data structure:** Efficient for prefix operations (advanced)

---

## 6️⃣ **String Matching / Searching** ⭐

### 🎓 When to Use
- **Keywords:** "find substring", "pattern", "needle in haystack", "repeated substring"
- **Recognition:** Need to locate pattern in text

### 📝 Curated Problems

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 96 | Implement strStr() | Easy | [LeetCode 28](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/) | `built-in find`, `KMP O(n+m)`, `Rabin-Karp` |
| 97 | Repeated Substring Pattern | Easy | [LeetCode 459](https://leetcode.com/problems/repeated-substring-pattern/) | `try all divisors`, `(s+s)[1:-1].find(s)` trick |
| 98 | Shortest Palindrome | Hard | [LeetCode 214](https://leetcode.com/problems/shortest-palindrome/) | `KMP`, `reverse and match`, `add prefix` |

**🔑 Key Tricks:**
- **Naive:** O(n*m) sliding window comparison
- **KMP Algorithm:** O(n+m) using failure function (build LPS array)
- **Rabin-Karp:** Rolling hash for O(n+m) average case
- **Python:** Use built-in `s.find()` for simplicity

---

## 7️⃣ **Dynamic Programming on Strings** ⭐⭐⭐

### 🎓 When to Use
- **Keywords:** "longest palindrome", "edit distance", "longest common subsequence", "partition"
- **Recognition:** Optimization, counting, subsequence problems

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 99 | Longest Palindromic Substring | Medium | [LeetCode 5](https://leetcode.com/problems/longest-palindromic-substring/) | `expand around center`, `DP O(n²)`, `Manacher O(n)` |
| 100 | Palindromic Substrings | Medium | [LeetCode 647](https://leetcode.com/problems/palindromic-substrings/) | `expand around center`, `count all`, `odd/even length` |
| 101 | Longest Common Subsequence | Medium | [LeetCode 1143](https://leetcode.com/problems/longest-common-subsequence/) | `dp[i][j]`, `match: dp[i-1][j-1]+1`, `else: max()` |
| 102 | Edit Distance | Medium | [LeetCode 72](https://leetcode.com/problems/edit-distance/) | `dp[i][j]`, `insert/delete/replace`, `min operations` |
| 103 | Distinct Subsequences | Hard | [LeetCode 115](https://leetcode.com/problems/distinct-subsequences/) | `dp[i][j]`, `count ways`, `match vs skip` |
| 104 | Longest Palindromic Subsequence | Medium | [LeetCode 516](https://leetcode.com/problems/longest-palindromic-subsequence/) | `LCS(s, reverse(s))`, `dp[i][j]` |
| 105 | Palindrome Partitioning | Medium | [LeetCode 131](https://leetcode.com/problems/palindrome-partitioning/) | `backtracking`, `precompute palindrome table` |
| 106 | Palindrome Partitioning II | Hard | [LeetCode 132](https://leetcode.com/problems/palindrome-partitioning-ii/) | `dp for min cuts`, `palindrome checking` |
| 107 | Decode Ways | Medium | [LeetCode 91](https://leetcode.com/problems/decode-ways/) | `dp[i] = dp[i-1] + dp[i-2]`, `check valid 1 or 2 digits` |

**🔑 Key Tricks:**
- **Expand around center:** For palindrome substring/count (O(n²))
- **LCS pattern:** `dp[i][j] = dp[i-1][j-1] + 1` if match, else `max(dp[i-1][j], dp[i][j-1])`
- **Edit distance:** Three operations (insert, delete, replace)
- **Subsequence vs substring:** Subsequence can skip, substring is consecutive
- **Precompute palindromes:** Use DP table `isPalin[i][j]` for efficiency

---

## 8️⃣ **Stack Pattern (Strings)** ⭐

### 🎓 When to Use
- **Keywords:** "parentheses", "brackets", "valid", "decode", "remove duplicates", "calculator"
- **Recognition:** Need to match pairs or process in LIFO order

### 📝 Curated Problems (MUST MASTER)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 108 | Valid Parentheses | Easy | [LeetCode 20](https://leetcode.com/problems/valid-parentheses/) | `stack`, `push open`, `pop and match close`, `hashmap pairs` |
| 109 | Remove All Adjacent Duplicates | Easy | [LeetCode 1047](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/) | `stack`, `pop if top matches`, `else push` |
| 110 | Remove K Digits | Medium | [LeetCode 402](https://leetcode.com/problems/remove-k-digits/) | `monotonic increasing stack`, `greedy`, `remove larger digits` |
| 111 | Simplify Path | Medium | [LeetCode 71](https://leetcode.com/problems/simplify-path/) | `split by /`, `stack for directories`, `handle . and ..` |
| 112 | Decode String | Medium | [LeetCode 394](https://leetcode.com/problems/decode-string/) | `stack of (count, string)`, `nested encoding` |
| 113 | Basic Calculator | Hard | [LeetCode 224](https://leetcode.com/problems/basic-calculator/) | `stack for numbers`, `handle +/- signs`, `parentheses` |
| 114 | Basic Calculator II | Medium | [LeetCode 227](https://leetcode.com/problems/basic-calculator-ii/) | `stack`, `handle */ first`, `+/- later` |

**🔑 Key Tricks:**
- **Valid parentheses:** Push opening brackets, pop and match closing
- **Remove duplicates:** Stack top comparison, pop if match
- **Monotonic stack:** For greedy removal (keep increasing/decreasing)
- **Nested structures:** Stack tracks levels (decode string, calculator)
- **Two stacks:** One for operands, one for operators (calculator)

---

## 9️⃣ **Advanced String Patterns**

### 📝 A. Expand Around Center (Palindromes)

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 115 | Longest Palindromic Substring | Medium | [LeetCode 5](https://leetcode.com/problems/longest-palindromic-substring/) | `expand from each center`, `odd/even length`, `O(n²)` |
| 116 | Palindromic Substrings | Medium | [LeetCode 647](https://leetcode.com/problems/palindromic-substrings/) | `expand and count`, `each index as center` |

**🔑 Key Trick:** Try each position as center, expand left and right while characters match

---

### 📝 B. Greedy String Problems

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 117 | Reorganize String | Medium | [LeetCode 767](https://leetcode.com/problems/reorganize-string/) | `max heap`, `frequency count`, `place most frequent first` |
| 118 | Remove Duplicate Letters | Medium | [LeetCode 316](https://leetcode.com/problems/remove-duplicate-letters/) | `stack`, `greedy`, `track last occurrence`, `seen set` |
| 119 | Smallest Subsequence of Distinct Chars | Medium | [LeetCode 1081](https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/) | `same as 316`, `monotonic stack` |

---

### 📝 C. String Transformation

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 120 | One Edit Distance | Medium | [LeetCode 161](https://leetcode.com/problems/one-edit-distance/) | `length difference`, `check insert/delete/replace` |
| 121 | Compare Version Numbers | Medium | [LeetCode 165](https://leetcode.com/problems/compare-version-numbers/) | `split by .`, `compare integers`, `pad with zeros` |
| 122 | Multiply Strings | Medium | [LeetCode 43](https://leetcode.com/problems/multiply-strings/) | `digit-by-digit`, `carry`, `reverse result` |

---

### 📝 D. Regex / Pattern Matching

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 123 | Regular Expression Matching | Hard | [LeetCode 10](https://leetcode.com/problems/regular-expression-matching/) | `DP`, `handle . and *`, `match or skip` |
| 124 | Wildcard Matching | Hard | [LeetCode 44](https://leetcode.com/problems/wildcard-matching/) | `DP`, `handle ? and *`, `greedy backtracking` |

---

### 📝 E. Substring Variants

| # | Problem | Difficulty | Link | Keywords/Tricks |
|---|---------|-----------|------|-----------------|
| 125 | Longest Substring with At Least K Repeating | Medium | [LeetCode 395](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/) | `divide and conquer`, `split at invalid chars` |
| 126 | Count and Say | Medium | [LeetCode 38](https://leetcode.com/problems/count-and-say/) | `simulation`, `count consecutive`, `build next` |

---

# 📊 PATTERN RECOGNITION GUIDE

---

## 🎯 How to Identify the Right Pattern

### 🔍 Pattern Decision Tree

```
INPUT TYPE
├─ Is array/string SORTED?
│  ├─ YES → Try: Two Pointer, Binary Search
│  └─ NO → Consider: Hashing, Sorting First
│
├─ Need to find SUBARRAY/SUBSTRING?
│  ├─ Fixed size → Sliding Window (Fixed)
│  ├─ Variable size with constraints → Sliding Window (Variable)
│  ├─ Sum equals K → Prefix Sum + Hashmap
│  └─ All subarrays → Nested loops or DP
│
├─ Need PAIRS/TRIPLETS?
│  ├─ Sorted → Two Pointer
│  ├─ Unsorted → Hashmap or Sort First
│  └─ Complement needed → Hashmap
│
├─ Need FREQUENCY/COUNT?
│  └─ Hashmap / Frequency Array
│
├─ Need OPTIMIZATION (max/min/count)?
│  ├─ Overlapping subproblems → DP
│  ├─ Greedy works → Greedy
│  └─ Try all combinations → Backtracking
│
├─ INTERVALS/MERGING?
│  └─ Sort by start → Merge
│
├─ PALINDROME?
│  ├─ Check → Two Pointer
│  ├─ Find all → Expand Around Center
│  └─ Optimize → DP
│
├─ PARENTHESES/MATCHING?
│  └─ Stack
│
├─ NEXT GREATER/SMALLER?
│  └─ Monotonic Stack
│
└─ SEARCH in specific range?
   └─ Binary Search (if monotonic)
```

---

## 🔑 Keyword → Pattern Mapping

| **Keywords in Problem** | **Likely Pattern(s)** |
|-------------------------|-----------------------|
| "sorted array" | Two Pointer, Binary Search |
| "subarray", "substring" | Sliding Window, Prefix Sum |
| "sum equals k" | Prefix Sum + Hashmap |
| "maximum", "minimum" | DP, Greedy, Kadane's |
| "pair", "two numbers" | Two Pointer, Hashmap |
| "duplicate", "unique" | Hashmap, Set |
| "frequency", "count" | Hashmap, Frequency Array |
| "consecutive" | Union Find, Hashmap |
| "longest", "shortest" | DP, Sliding Window |
| "palindrome" | Two Pointer, Expand Around Center, DP |
| "anagram" | Hashmap, Sorting |
| "parentheses", "brackets" | Stack |
| "next greater/smaller" | Monotonic Stack |
| "intervals", "merge" | Sort + Merge |
| "rotated" | Modified Binary Search |
| "subsequence" | DP, Two Pointer |
| "edit", "transform" | DP (Edit Distance) |
| "decode", "nested" | Stack, Recursion |
| "at most K" | Sliding Window |
| "partition" | DP, Backtracking |

---

## 💡 Common Tricks to Remember

### Arrays
1. **Two Sum variants:** Use hashmap for O(n) solution
2. **Kadane's Algorithm:** Maximum subarray in O(n)
3. **Dutch National Flag:** Three-way partitioning in one pass
4. **Binary Search on Answer:** When answer is in a range, check feasibility
5. **Prefix Sum trick:** `sum(i,j) = prefix[j] - prefix[i-1]`
6. **Monotonic Stack:** For next greater/smaller in O(n)
7. **Sliding Window Maximum:** Use deque to maintain max in window

### Strings
1. **Anagram check:** Sort or frequency map
2. **Palindrome:** Two pointer from ends or expand from center
3. **Valid Parentheses:** Stack with hashmap for pairs
4. **LCS (Longest Common Subsequence):** 2D DP, `dp[i][j]`
5. **Edit Distance:** 3 operations (insert, delete, replace)
6. **KMP Algorithm:** Linear string matching with failure function
7. **Sliding Window + Hashmap:** For substring with constraints

---

## 🎓 Learning Strategy

### 📅 Suggested 8-Week Study Plan

#### **Weeks 1-2: Foundations**
- Master basic array/string operations
- Learn sorting algorithms
- Practice two pointer pattern (15-20 problems)
- Understand time/space complexity

#### **Weeks 3-4: Core Patterns**
- Sliding Window (15-20 problems)
- Prefix Sum (10-15 problems)
- Hashing/Frequency Count (15-20 problems)
- Binary Search (15-20 problems)

#### **Weeks 5-6: Advanced Patterns**
- Dynamic Programming on arrays/strings (20-25 problems)
- Stack patterns (10-15 problems)
- Merge/Partition (10 problems)
- String matching algorithms

#### **Weeks 7-8: Special Techniques & Mixed**
- Monotonic Stack (8-10 problems)
- Advanced DP (palindromes, edit distance)
- Mixed pattern problems
- Mock interviews and timed contests

---

## 🚀 Problem-Solving Framework

### Step-by-Step Approach

1. **Understand the Problem**
   - Read carefully, understand constraints
   - Identify input/output format
   - Note edge cases (empty, single element, all same)

2. **Pattern Recognition**
   - Look for keywords (sorted, subarray, frequency, etc.)
   - Check the decision tree above
   - Consider multiple approaches

3. **Plan the Solution**
   - Choose appropriate data structure
   - Decide on algorithm/pattern
   - Consider time/space complexity

4. **Implement**
   - Write clean, readable code
   - Handle edge cases
   - Use meaningful variable names

5. **Test & Optimize**
   - Test with examples
   - Check edge cases
   - Optimize if needed (space/time trade-offs)

---

## 📈 Difficulty Progression

### Easy → Medium → Hard
- **Easy:** Focus on understanding pattern basics
- **Medium:** Combine multiple patterns, add constraints
- **Hard:** Complex variations, optimal solutions required

### Practice Strategy
- Master **Easy** problems first (build confidence)
- Move to **Medium** (where most interviews focus)
- Attempt **Hard** for deeper understanding (not always needed)

---

## 🎯 Interview Tips

1. **Clarify Requirements:** Ask questions before coding
2. **Think Aloud:** Explain your thought process
3. **Start Simple:** Brute force first, then optimize
4. **Test Your Code:** Walk through with examples
5. **Know Complexity:** Always state time/space complexity
6. **Practice Coding:** On whiteboard or online editors
7. **Time Management:** Don't spend too long on one problem

---

## 📚 Additional Resources

### Online Judges
- [LeetCode](https://leetcode.com/) - Primary platform
- [HackerRank](https://www.hackerrank.com/)
- [Codeforces](https://codeforces.com/)
- [CodeChef](https://www.codechef.com/)

### Learning Platforms
- [NeetCode](https://neetcode.io/) - Curated problem lists
- [AlgoExpert](https://www.algoexpert.io/)
- [Educative](https://www.educative.io/)

### Books
- "Cracking the Coding Interview" by Gayle Laakmann McDowell
- "Elements of Programming Interviews" by Adnan Aziz
- "Algorithm Design Manual" by Steven Skiena

---

## ✅ Progress Tracking

### Checklist by Pattern

**Arrays:**
- [ ] Two Pointer (15+ problems)
- [ ] Sliding Window (15+ problems)
- [ ] Prefix Sum (10+ problems)
- [ ] Hashing (15+ problems)
- [ ] Binary Search (15+ problems)
- [ ] Dynamic Programming (15+ problems)
- [ ] Merge/Partition (8+ problems)
- [ ] Monotonic Stack (8+ problems)

**Strings:**
- [ ] Two Pointer (10+ problems)
- [ ] Hashing (10+ problems)
- [ ] Sliding Window (10+ problems)
- [ ] String Matching (5+ problems)
- [ ] Dynamic Programming (10+ problems)
- [ ] Stack (10+ problems)
- [ ] Expand Around Center (5+ problems)

---

## 🎉 Final Words

> **Consistency > Intensity**
>
> Solve **2-3 problems daily** rather than 20 problems once a week.
> 
> **Understand > Memorize**
>
> Focus on understanding patterns and approaches, not memorizing solutions.
>
> **Review > Move On**
>
> Revisit problems after a week to reinforce learning.

---

## 📝 Notes Section

Use this space to add your own insights, tricks, or problem variations as you progress:

```
Problem: _____________________
Pattern: _____________________
Key Insight: _________________
Time Complexity: _____________
Space Complexity: ____________
Mistakes Made: _______________
```

---

**Created with ❤️ for aspiring problem solvers**

*Last Updated: 2025*

---

**Happy Coding! 🚀**
