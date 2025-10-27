
---

# 🎨 LeetCode 75 — Sort Colors

---

### 🧠 1. Problem Understanding (Simplified)

We’re given an array `nums` containing only **0s, 1s, and 2s**, representing colors:

* 0 → Red
* 1 → White
* 2 → Blue

We need to **sort the array in-place** so that all 0s come first, then 1s, then 2s.
(You **cannot use built-in sort** — do it manually.)

✅ **Goal:** Modify `nums` directly to be sorted in ascending order.

---

### 🔍 Example

**Input:**
`nums = [2, 0, 2, 1, 1, 0]`

**Output:**
`[0, 0, 1, 1, 2, 2]`

**Explanation:**
All red (0) first → white (1) next → blue (2) last.

---

### ⚙️ 2. Example Visualization

Before: `[2, 0, 2, 1, 1, 0]`
After:  `[0, 0, 1, 1, 2, 2]`

We just need to **rearrange the same array** — no new array creation allowed.

---

## 🧩 3. Approach 1 — Brute Force (Counting Sort)

This is the most straightforward way.

### 💡 Idea

1. Count how many 0s, 1s, and 2s are in the array.
2. Overwrite the array with that many 0s, then 1s, then 2s.

---

### 🧾 Code — Brute Force (Counting Sort)

```python
class Solution:
    def sortColors(self, nums: list[int]) -> None:
        count0 = count1 = count2 = 0
        
        # Count occurrences
        for num in nums:
            if num == 0:
                count0 += 1
            elif num == 1:
                count1 += 1
            else:
                count2 += 1
        
        # Overwrite nums
        index = 0
        for _ in range(count0):
            nums[index] = 0
            index += 1
        for _ in range(count1):
            nums[index] = 1
            index += 1
        for _ in range(count2):
            nums[index] = 2
            index += 1
```

---

### 🧩 What it means

In Python, this line **assigns the same value (`0`) to multiple variables at once**.

So this:

```python
count0 = count1 = count2 = 0
```

is equivalent to writing:

```python
count0 = 0
count1 = 0
count2 = 0
```

✅ All three variables get the value `0`.
They are **not separated by commas** because it’s **one chained assignment statement**, not a tuple.

---

### ⚙️ Why not use commas?

If you tried:

```python
count0, count1, count2 = 0
```

❌ You’d get an error — because the right-hand side (`0`) isn’t iterable (it can’t be unpacked into three variables).

If you wrote:

```python
count0, count1, count2 = 0, 0, 0
```

✅ That also works — it’s called **tuple unpacking**.

But the difference is:

| Syntax                             | Meaning                         | Works?  |
| ---------------------------------- | ------------------------------- | ------- |
| `count0 = count1 = count2 = 0`     | Assigns same value (`0`) to all | ✅ Yes   |
| `count0, count1, count2 = 0, 0, 0` | Assigns values position-wise    | ✅ Yes   |
| `count0, count1, count2 = 0`       | Unpack 1 value into 3 vars      | ❌ Error |

---
Perfect — you’re asking for a **dry run explanation** of this code block 👇

```python
index = 0

for _ in range(count0):
    nums[index] = 0
    index += 1

for _ in range(count1):
    nums[index] = 1
    index += 1

for _ in range(count2):
    nums[index] = 2
    index += 1
```


Example:

```python
nums = [2, 0, 2, 1, 1, 0]
```

After counting:

```
count0 = 2  # number of 0s
count1 = 2  # number of 1s
count2 = 2  # number of 2s
```

---

### ⚙️ **Purpose of this code**

This part **rewrites the array** in sorted order, based on the counts found earlier.

---

### 🧮 **Dry Run Step-by-Step**

#### Initial State:

```
nums  = [2, 0, 2, 1, 1, 0]
count0 = 2
count1 = 2
count2 = 2
index = 0
```

---

#### 🧱 First loop — Fill all 0s

```python
for _ in range(count0):   # runs 2 times
```

* **1st iteration** → `nums[0] = 0`, then `index = 1`
* **2nd iteration** → `nums[1] = 0`, then `index = 2`

After first loop:

```
nums = [0, 0, 2, 1, 1, 0]
index = 2
```

---

#### ⚪ Second loop — Fill all 1s

```python
for _ in range(count1):   # runs 2 times
```

* **1st iteration** → `nums[2] = 1`, then `index = 3`
* **2nd iteration** → `nums[3] = 1`, then `index = 4`

After second loop:

```
nums = [0, 0, 1, 1, 1, 0]
index = 4
```

---

#### 🔵 Third loop — Fill all 2s

```python
for _ in range(count2):   # runs 2 times
```

* **1st iteration** → `nums[4] = 2`, then `index = 5`
* **2nd iteration** → `nums[5] = 2`, then `index = 6`

After third loop:

```
nums = [0, 0, 1, 1, 2, 2]
index = 6
```

✅ **Final Output:** `[0, 0, 1, 1, 2, 2]`

---

### 🧠 **Logic Summary**

| Loop | What it does | Runs           | Value inserted | Example array        |
| ---- | ------------ | -------------- | -------------- | -------------------- |
| 1️⃣  | Fill all 0s  | `count0` times | `0`            | `[0, 0, …]`          |
| 2️⃣  | Fill all 1s  | `count1` times | `1`            | `[0, 0, 1, 1, …]`    |
| 3️⃣  | Fill all 2s  | `count2` times | `2`            | `[0, 0, 1, 1, 2, 2]` |

---

| Symbol | Purpose                           | When to use                                    |
| :----- | :-------------------------------- | :--------------------------------------------- |
| `_`    | “I don’t need this loop variable” | When variable is unused                        |
| `i`    | “I might use this variable”       | When you want to use its value inside the loop |


---

## 🧮 Example

Let’s assume:

```python
count0 = 3
```

Now look at this:

```python
for i in range(count0):
    print(i)
```

🖨 **Output:**

```
0
1
2
```

If you used `_` instead:

```python
for _ in range(count0):
    print("Filling 0s")
```

🖨 **Output:**

```
Filling 0s
Filling 0s
Filling 0s
```

So `i` gives you a **real index value** (`0, 1, 2...`)
but `_` means **“I don’t care what the value is” — just repeat.**

---

### ⚠️ Why `_` is preferred here

In this part of the **Sort Colors algorithm**:

```python
for _ in range(count0):
    nums[index] = 0
    index += 1
```

We don’t use the loop variable at all — so `_` is just **cleaner** and signals that fact.

Using `i` would still work, but a good programmer reading your code might think:

> “Hmm, maybe `i` is used somewhere later,”
> when it’s actually not.
---

### ⏱️ Time & Space Complexity

| Operation | Complexity |
| --------- | ---------- |
| Time      | O(n)       |
| Space     | O(1)       |

✅ Efficient but **not truly one-pass** (two separate traversals).

---

## ⚙️ 4. Approach 2 — Dutch National Flag (Optimal — One Pass)

This is the classic and **most optimal** way.

---

### 💡 Core Idea

Use **three pointers**:

* `low` — boundary for 0s
* `mid` — current element pointer
* `high` — boundary for 2s

Initially:

```
low = 0
mid = 0
high = len(nums) - 1
```

We process `mid` and decide:

* If `nums[mid] == 0` → swap with `nums[low]`, move both `low` and `mid` forward.
* If `nums[mid] == 1` → correct place, just move `mid` forward.
* If `nums[mid] == 2` → swap with `nums[high]`, move `high` backward.

---

### 🧾 Code — Optimal (Dutch National Flag)

```python
class Solution:
    def sortColors(self, nums: list[int]) -> None:
        low, mid, high = 0, 0, len(nums) - 1
        
        while mid <= high:
            if nums[mid] == 0:
                nums[low], nums[mid] = nums[mid], nums[low]
                low += 1
                mid += 1
            elif nums[mid] == 1:
                mid += 1
            else:  # nums[mid] == 2
                nums[mid], nums[high] = nums[high], nums[mid]
                high -= 1
```

---



We must **sort them in-place** so that:

```
All 0s → come first
All 1s → come next
All 2s → come last
```

Example:

```
Input:  [2, 0, 2, 1, 1, 0]
Output: [0, 0, 1, 1, 2, 2]
```

---

## ⚙️ Algorithm Overview — Dutch National Flag

We use **three pointers**:

| Pointer | Meaning                        | Starts at |
| ------- | ------------------------------ | --------- |
| `low`   | boundary for next 0            | 0         |
| `mid`   | current element we’re checking | 0         |
| `high`  | boundary for next 2            | n - 1     |

Rules inside the `while mid <= high:` loop:

| nums[mid] value | Action                          | Pointer Movement       |
| --------------- | ------------------------------- | ---------------------- |
| 0               | Swap `nums[low]` ↔ `nums[mid]`  | `low += 1`, `mid += 1` |
| 1               | Leave it as is                  | `mid += 1`             |
| 2               | Swap `nums[mid]` ↔ `nums[high]` | `high -= 1`            |

---

## 🧮 Dry Run Example

Input:

```python
nums = [2, 0, 2, 1, 1, 0]
```

Initial pointers:

```
low = 0
mid = 0
high = 5
```

---

### **🔹 Step 1**

```
nums[mid] = 2
```

Swap `nums[mid]` ↔ `nums[high]`

```
nums = [0, 0, 2, 1, 1, 2]
                ↑       ↑
               mid     high
```

Now:

```
high -= 1  →  high = 4
(mid stays same → recheck nums[mid])
```

---

### **🔹 Step 2**

```
nums[mid] = 0
```

Swap `nums[low]` ↔ `nums[mid]`

```
nums = [0, 0, 2, 1, 1, 2]
          ↑  ↑
         low mid
```

Then:

```
low += 1 → 1
mid += 1 → 1
```

---

### **🔹 Step 3**

```
nums[mid] = 0
```

Swap again `nums[low]` ↔ `nums[mid]` (same position, so no visible change)

```
nums = [0, 0, 2, 1, 1, 2]
             ↑  ↑
            low mid
```

Then:

```
low = 2
mid = 2
```

---

### **🔹 Step 4**

```
nums[mid] = 2
```

Swap `nums[mid]` ↔ `nums[high]`

```
nums = [0, 0, 1, 1, 2, 2]
                ↑     ↑
               mid   high
```

Then:

```
high = 3
(mid stays same)
```

---

### **🔹 Step 5**

```
nums[mid] = 1
```

→ Leave as is

```
mid += 1 → 3
```

---

### **🔹 Step 6**

```
nums[mid] = 1
```

→ Leave as is

```
mid += 1 → 4
```

Now loop ends since:

```
mid (4) > high (3)
```

---

✅ **Final Array:**

```
[0, 0, 1, 1, 2, 2]
```

---

## 🧭 Visual Summary Diagram

| Step | low | mid | high | nums[mid] | Action                      | Array         |
| ---- | --- | --- | ---- | --------- | --------------------------- | ------------- |
| 1    | 0   | 0   | 5    | 2         | Swap mid↔high → high–       | [0,0,2,1,1,2] |
| 2    | 0   | 0   | 4    | 0         | Swap low↔mid → low++, mid++ | [0,0,2,1,1,2] |
| 3    | 1   | 1   | 4    | 0         | Swap low↔mid → low++, mid++ | [0,0,2,1,1,2] |
| 4    | 2   | 2   | 4    | 2         | Swap mid↔high → high–       | [0,0,1,1,2,2] |
| 5    | 2   | 2   | 3    | 1         | mid++                       | [0,0,1,1,2,2] |
| 6    | 2   | 3   | 3    | 1         | mid++                       | [0,0,1,1,2,2] |

---

## 🧠 Intuition Summary

* `low` → marks the boundary for where **0s** should go
* `mid` → scans and checks the elements
* `high` → marks the boundary for where **2s** should go
* Everything **left of low = 0s**, **right of high = 2s**, and **mid moves until done**

---


---

### 📊 6. Time & Space Analysis

| Approach            | Time | Space | Notes                          |
| ------------------- | ---- | ----- | ------------------------------ |
| Counting Sort       | O(n) | O(1)  | Two passes                     |
| Dutch National Flag | O(n) | O(1)  | ✅ One pass, best for interview |

---

### 🧪 7. Quick Test Cases

```python
sol = Solution()

nums = [2, 0, 2, 1, 1, 0]
sol.sortColors(nums)
print(nums)  # ✅ [0, 0, 1, 1, 2, 2]

nums = [2, 0, 1]
sol.sortColors(nums)
print(nums)  # ✅ [0, 1, 2]

nums = [0]
sol.sortColors(nums)
print(nums)  # ✅ [0]

nums = [1, 2, 0]
sol.sortColors(nums)
print(nums)  # ✅ [0, 1, 2]
```

---

### 🧠 8. Summary Comparison

| Approach                | Description                        | Time | Space | Remarks               |
| ----------------------- | ---------------------------------- | ---- | ----- | --------------------- |
| **Brute Force**         | Count 0s, 1s, 2s separately        | O(n) | O(1)  | Easy to understand    |
| **Dutch National Flag** | One-pass, in-place, three pointers | O(n) | O(1)  | ✅ Best for interviews |

---

### 💬 9. Final Takeaway

* **Understand pattern:** only 3 values → partition into 3 zones
* **Pointer roles:**

  * `low` → boundary for 0s
  * `mid` → current checker
  * `high` → boundary for 2s
* Always ensure:

  * Left zone → 0s
  * Middle zone → 1s
  * Right zone → 2s

---

✅ **In Interviews:**
If you implement Dutch National Flag correctly and explain pointer movement logic clearly — you’ll easily score **full marks** on this question.

Would you like me to make a **visual diagram** (step-by-step color box movement) for this next? It helps you remember the pointer transitions instantly.
