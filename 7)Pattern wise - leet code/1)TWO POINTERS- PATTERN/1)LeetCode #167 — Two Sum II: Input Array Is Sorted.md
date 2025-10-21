
---

# 🧭 LeetCode #167 — Two Sum II: Input Array Is Sorted

---

## 🧩 1. Problem Understanding (In Simple Words)

**You are given:**

* An array of integers called `numbers`.
* This array is **sorted** in non-decreasing order (which means each next number is greater than or equal to the previous one).
* A target integer value called `target`.

**You need to find:**
Two numbers in this array that **add up exactly** to `target`.

You must return their **indices** as a list `[i, j]`.

---

### ⚠️ Important Rules

| Rule                 | Meaning                                                                                                         |
| -------------------- | --------------------------------------------------------------------------------------------------------------- |
| `1 ≤ i < j ≤ n`      | Choose two different positions `i` and `j`, where both are inside the array (1 to n), and `i` comes before `j`. |
| 1-based indexing     | The array positions start at 1 in the **answer** (but remember: in Python, actual indices start at 0).          |
| Exactly one solution | You will always find one valid pair that adds up to `target`.                                                   |
| Constant extra space | You can’t use extra memory like a dictionary — solution should use O(1) extra space.                            |

---

### 💡 Example 1

**Input:**

```python
numbers = [2, 7, 11, 15]
target = 9
```

**Output:**

```python
[1, 2]
```

**Explanation:**

* numbers[0] = 2
* numbers[1] = 7
  → 2 + 7 = 9 ✅
  So, the answer is `[1, 2]` (1-based index → add +1 to both positions).

---

### 💡 Example 2

**Input:**

```python
numbers = [2, 3, 4]
target = 6
```

**Output:**

```python
[1, 3]
```

**Why:**
2 + 4 = 6 ✅
Indices (0, 2) → return `[1, 3]`.

---

### 💡 Example 3

**Input:**

```python
numbers = [-1, 0]
target = -1
```

**Output:**

````python
[1, 2]```

**Why:**  
(-1) + (0) = -1 ✅

---

## 🧮 2. Understanding “1 ≤ i < j ≤ n”

Let’s decode this line 👇  

- `1 ≤ i` → `i` starts from position 1 (first element).
- `i < j` → both indices must be different, and `i` must come **before** `j`.
- `j ≤ n` → `j` cannot go beyond the end of the array (where `n` = total elements).

So in English:
> “Pick two different elements from the array where the first comes before the second.”

Example for `numbers = [2, 7, 11, 15]` (n = 4):
Possible pairs are:
````

(1,2), (1,3), (1,4), (2,3), (2,4), (3,4)

````

---

## 🔍 3. Why the “Sorted” Property Matters

Since the array is sorted:
- If the sum of two numbers is **too small**, we can move the **left pointer** right (to increase the sum).
- If the sum is **too big**, we can move the **right pointer** left (to decrease the sum).

This sorted order lets us find the answer **without checking every pair**.

That’s the **core idea** behind the **Two Pointer technique**.  

---

## ⚙️ 4. Step-by-Step Solution Approaches

---

### 🪜 **Approach 1 — Brute Force (Beginners’ First Try)**

---

#### 🔧 Idea:
Try **every possible pair** `(i, j)` and check if they add up to `target`.

If yes → return their indices.

---

#### 🧠 Thought Process:
- Loop through every element using index `i`.
- For every `i`, loop through all elements **after it** using index `j`.
- Check if `numbers[i] + numbers[j] == target`.

If true → return `[i+1, j+1]` (because answer must be 1-based).

---

#### 🧾 Code:
```python
def twoSum(numbers, target):
    n = len(numbers)
    for i in range(n):
        for j in range(i + 1, n):
            if numbers[i] + numbers[j] == target:
                return [i + 1, j + 1]
````


---

## The Code You Shared

```python
n = len(numbers)
for i in range(n):
    for j in range(i + 1, n):
        # do something with numbers[i] and numbers[j]
```

We are talking about **Two Sum II brute force approach**, where we check **every possible pair** of numbers.

---

## 1️⃣ What is `range(n)`?

* `n = len(numbers)` → `n` is the **number of elements** in the array `numbers`.
* `range(n)` → generates numbers from `0` to `n-1` (because Python arrays are **0-indexed**).

Example:

```python
numbers = [2, 7, 11, 15]
n = len(numbers)  # 4
range(n)           # 0, 1, 2, 3
```

---

## 2️⃣ Outer Loop: `for i in range(n)`

```python
for i in range(n):
    # something
```

* This loop **goes through each element** in the array from **start to end**.
* `i` is the **index** of the current element.

Example:

```python
numbers = [2, 7, 11, 15]
for i in range(len(numbers)):
    print(i, numbers[i])
```

**Output:**

```
0 2
1 7
2 11
3 15
```

✅ So the outer loop picks **one element at a time**.

---

## 3️⃣ Inner Loop: `for j in range(i + 1, n)`

```python
for j in range(i + 1, n):
    # do something with numbers[i] and numbers[j]
```

* For **every outer loop element** (`numbers[i]`), the inner loop picks **all the elements that come after it**.
* `j = i + 1` ensures we **don’t check the same element twice** and that `i < j`.
* `range(i + 1, n)` → numbers from `i+1` to `n-1`.

---

### Step-by-step Example

Array: `[2, 7, 11, 15]`
`n = 4`

**Outer Loop i = 0 → numbers[i] = 2**

Inner loop `j` goes from `i+1 = 1` to `3`:

| j | numbers[j] | Pair Checked |
| - | ---------- | ------------ |
| 1 | 7          | (2, 7) ✅     |
| 2 | 11         | (2, 11)      |
| 3 | 15         | (2, 15)      |

---

**Outer Loop i = 1 → numbers[i] = 7**

Inner loop `j` goes from `2` to `3`:

| j | numbers[j] | Pair Checked |
| - | ---------- | ------------ |
| 2 | 11         | (7, 11)      |
| 3 | 15         | (7, 15)      |

---

**Outer Loop i = 2 → numbers[i] = 11**

Inner loop `j` goes from `3` to `3`:

| j | numbers[j] | Pair Checked |
| - | ---------- | ------------ |
| 3 | 15         | (11, 15)     |

---

**Outer Loop i = 3 → numbers[i] = 15**

Inner loop `j` goes from `4` to `3` → **does not run**, because start > end.

---

✅ So all **possible pairs (i, j)** are:

```
(2, 7), (2, 11), (2, 15), (7, 11), (7, 15), (11, 15)
```

Exactly what we need for **brute-force Two Sum**.

---

## 4️⃣ Visual Representation

```
Outer Loop (i)
2  → Inner Loop j: 7, 11, 15
7  → Inner Loop j: 11, 15
11 → Inner Loop j: 15
15 → Inner Loop j: none
```

---

## 5️⃣ Why do we use `i + 1` in inner loop?

* We **don’t want to pair a number with itself** (like 2+2).
* We **don’t want to repeat pairs** (like 7+2, which is same as 2+7 in sum).

So `j` always starts **right after `i`**.

---

## 6️⃣ How It Works in Brute-Force Two Sum

```python
for i in range(n):
    for j in range(i + 1, n):
        if numbers[i] + numbers[j] == target:
            return [i + 1, j + 1]  # 1-based indexing
```

* Outer loop picks **first number**.
* Inner loop checks **all numbers after it** to see if sum = target.
* As soon as we find a match → **return indices**.

✅ Works for small arrays, but **O(n²)** — slow for very large arrays.

---

If you want, I can **draw a simple diagram showing i and j pointers moving**, so it becomes **instantly clear** even for beginners.

Do you want me to do that?

---

#### 🧮 Example walkthrough

Input:

```
numbers = [2, 7, 11, 15], target = 9
```

* i = 0, j = 1 → 2 + 7 = 9 ✅
  Return `[1, 2]`

---

#### ⏱️ Time & Space:

| Metric | Complexity                                                 |
| ------ | ---------------------------------------------------------- |
| Time   | O(n²) — because for each element, we look through the rest |
| Space  | O(1) — we’re not using any extra array                     |

✅ Works fine for small arrays,
❌ Too slow for large arrays (n up to 30,000 here).

---

### ⚡ **Approach 2 — Optimal Two Pointer Solution**

---

#### 🧠 Core Idea:

Because the array is **sorted**, we can use **two pointers**:

* `left` starts at the **beginning** (smallest number)
* `right` starts at the **end** (largest number)

We keep adjusting them until their sum equals `target`.

---

#### 🪜 Step-by-step logic:

1. Start:

   ```python
   left = 0
   right = len(numbers) - 1
   ```

2. While `left < right`:

   * Calculate current sum:

     ```python
     current_sum = numbers[left] + numbers[right]
     ```

   * If `current_sum == target` → we found our answer ✅
     Return `[left + 1, right + 1]`.

   * If `current_sum < target` → the sum is **too small**,
     → move `left` pointer **right** to increase the sum.

   * If `current_sum > target` → the sum is **too big**,
     → move `right` pointer **left** to decrease the sum.

---

#### 🧾 Code:

```python
def twoSum(numbers, target):
    left = 0
    right = len(numbers) - 1
    
    while left < right:
        current_sum = numbers[left] + numbers[right]
        
        if current_sum == target:
            return [left + 1, right + 1]  # +1 because question expects 1-based index
        elif current_sum < target:
            left += 1  # need a bigger sum
        else:
            right -= 1  # need a smaller sum
```

---

#### 🧮 Example walkthrough

Input:

```
numbers = [2, 7, 11, 15], target = 9
```

| Step | left | right | numbers[left] | numbers[right] | sum | Action               |
| ---- | ---- | ----- | ------------- | -------------- | --- | -------------------- |
| 1    | 0    | 3     | 2             | 15             | 17  | Too big → move right |
| 2    | 0    | 2     | 2             | 11             | 13  | Too big → move right |
| 3    | 0    | 1     | 2             | 7              | 9   | ✅ Found target!      |

Return `[1, 2]`.

---

#### ⏱️ Time & Space:

| Metric | Complexity                            |
| ------ | ------------------------------------- |
| Time   | O(n) — at most one pass through array |
| Space  | O(1) — only two pointers used         |

✅ **Very fast**
✅ **Constant extra space**
✅ **Perfectly fits the constraints**

---

## 🧠 5. Why Two Pointer Is the Best Choice

Let’s match it with problem clues:

| Problem Clue                          | Meaning                                    | Pattern        |
| ------------------------------------- | ------------------------------------------ | -------------- |
| “Sorted array”                        | You can move pointers logically left/right | ✅ Two Pointers |
| “Constant space”                      | No hash maps allowed                       | ✅ Two Pointers |
| “Exactly one solution”                | No need to handle duplicates or edge cases | ✅ Two Pointers |
| “Find two numbers that sum to target” | Pair search pattern                        | ✅ Two Pointers |

Everything fits — so this problem is **designed** for Two Pointer logic.

---

### 🪜 **Approach 3**(BINARY SEARCH)
---

---

## 💡 Core Idea

Since the array is **sorted**, we can use **binary search** instead of checking every pair.

For every element `numbers[i]`,
we find its **complement** = `target - numbers[i]`
by **binary searching** in the right portion of the array (from `i+1` to end).

If found → return indices
Else → continue with next `i`

---

## ⚙️ Code Breakdown

```python
for i in range(len(numbers)):    # loop each element
    left = i + 1                 # start searching from the next element
    right = len(numbers) - 1     # last index
    complement = target - numbers[i]   # number we need to reach target
```

We’ll now **binary search** for `complement` in `numbers[left:right+1]`.

---

### Binary Search Logic:

```python
while left <= right:
    mid = (left + right) // 2

    if numbers[mid] == complement:
        return [i + 1, mid + 1]     # found → 1-based index
    elif numbers[mid] < complement:
        left = mid + 1              # need bigger number → move right
    else:
        right = mid - 1             # need smaller number → move left
```

If the loop ends and no match → go to next `i`.

---

## 🧮 Dry Run Example

### Input:

```python
numbers = [2, 7, 11, 15]
target = 9
```

---

### Step 1️⃣  i = 0

* `numbers[i] = 2`
* `complement = 9 - 2 = 7`
* Search for `7` in `[7, 11, 15]`

| left | right | mid | numbers[mid] | comparison | action              |
| ---- | ----- | --- | ------------ | ---------- | ------------------- |
| 1    | 3     | 2   | 11           | 11 > 7     | right = mid - 1 = 1 |
| 1    | 1     | 1   | 7            | 7 == 7     | ✅ found             |

✅ Return `[i + 1, mid + 1] = [1, 2]`

---

### Step 2️⃣  (No need)

Loop exits because we already returned result.

---

## 🧠 Intuition of Why It Works

* Each `i` locks one number.
* Because the array is sorted, we can **quickly find** if its complement exists using **binary search** instead of scanning linearly.
* So instead of O(n²), we get O(n log n).

---

## 🧩 Complexity

| Metric    | Value                                                             |
| --------- | ----------------------------------------------------------------- |
| **Time**  | O(n log n) (loop over n elements, each binary search takes log n) |
| **Space** | O(1) (no extra structures)                                        |

---

## 🎮 How to “Play” with Binary Search

To *experiment* and “feel” how binary search behaves:

1. Print internal values inside the loop 👇

   ```python
   print(f"i={i}, left={left}, right={right}, mid={mid}, complement={complement}")
   ```

2. Try with different arrays and targets.
   Example:

   ```python
   numbers = [1, 3, 4, 5, 7, 11, 15]
   target = 10
   ```

   → you’ll see binary search narrowing down for `complement` each time.

3. Try arrays where the complement is at:

   * **beginning** of right half
   * **middle**
   * **end**
     to see how binary search moves pointers.

---

## 🏁 Summary

| Step                 | Meaning                       |
| -------------------- | ----------------------------- |
| Loop `i`             | Fix first number              |
| Compute `complement` | What you need to reach target |
| Binary search        | Check if complement exists    |
| Return indices       | Once found, stop              |

---


---

# ⚡ Quick Revision — Two Sum II (Sorted Array)

---

## 🥉 1️⃣ **Brute Force Approach**

### 💡 Logic:

Try **every possible pair (i, j)** and check if their sum equals target.

### 🧠 Steps:

```python
for i in range(len(numbers)):
    for j in range(i + 1, len(numbers)):
        if numbers[i] + numbers[j] == target:
            return [i + 1, j + 1]
```

### 🧩 Complexity:

| Type  | Value |
| ----- | ----- |
| Time  | O(n²) |
| Space | O(1)  |

### 🧠 Concept Summary:

* Simple but **slow**.
* Works even if array is **unsorted**.
* Avoid for large inputs.

🪫 Use only for **understanding** the problem.

---

## 🥈 2️⃣ **Binary Search Approach**

### 💡 Logic:

For each number, use **binary search** to find its complement (`target - numbers[i]`) in the right half.

### 🧠 Steps:

```python
for i in range(len(numbers)):
    left, right = i + 1, len(numbers) - 1
    complement = target - numbers[i]
    while left <= right:
        mid = (left + right) // 2
        if numbers[mid] == complement:
            return [i + 1, mid + 1]
        elif numbers[mid] < complement:
            left = mid + 1
        else:
            right = mid - 1
```

### 🧩 Complexity:

| Type  | Value      |
| ----- | ---------- |
| Time  | O(n log n) |
| Space | O(1)       |

### 🧠 Concept Summary:

* Exploits **sorted array** using binary search.
* **Loop + binary search** per element.
* Easier to visualize but slower than two-pointer.

⚙️ Use when you must use **binary search explicitly**.

---

## 🥇 3️⃣ **Two Pointer Approach (Optimal)**

### 💡 Logic:

Use **two pointers** — one from start (`left`) and one from end (`right`) — move them intelligently based on sum.

### 🧠 Steps:

```python
left, right = 0, len(numbers) - 1
while left < right:
    current_sum = numbers[left] + numbers[right]
    if current_sum == target:
        return [left + 1, right + 1]
    elif current_sum < target:
        left += 1
    else:
        right -= 1
```

### 🧩 Complexity:

| Type  | Value |
| ----- | ----- |
| Time  | O(n)  |
| Space | O(1)  |

### 🧠 Concept Summary:

* Uses **sorted property** perfectly.
* One pass → **fastest** solution.
* Clean and elegant.

🚀 Always choose this for sorted input arrays.

---

## 🔥 Final Comparison Table

| Rank | Approach      | Time       | Space | Key Idea                      | Best Use Case                       |
| ---- | ------------- | ---------- | ----- | ----------------------------- | ----------------------------------- |
| 🥇   | Two Pointer   | O(n)       | O(1)  | Move inward from both ends    | Sorted array                        |
| 🥈   | Binary Search | O(n log n) | O(1)  | Search complement per element | Sorted array, search practice       |
| 🥉   | Brute Force   | O(n²)      | O(1)  | Try every pair                | Very small inputs or unsorted array |

---

## 🧠 Quick Mnemonic to Remember

> **B → Binary**, **T → Two Pointer**, **B → Brute Force**
> **Speed Ranking:** 🐢 Brute Force < 🚶 Binary Search < 🚀 Two Pointer

---


