

---

# 🧩 **LeetCode 16 — 3Sum Closest**

This problem looks similar to the classic “3Sum,” but instead of finding *triplets that sum to zero*, we’re finding the **triplet whose sum is closest to a given target**.

We’ll cover:

1. Problem Understanding
2. Example Explanation
3. Approach 1 — Brute Force
4. Approach 2 — Two Pointers (Optimal)
5. Full Code with Comments (Optimal)
6. Dry Run (Step-by-Step Table)
7. Time & Space Analysis
8. Quick Test Cases
9. Summary Comparison

---

## 🧠 1. Problem Understanding (Simplified)

We’re given:

* An array of integers `nums`
* An integer `target`

We need to find **three numbers** in `nums` such that their sum is **closest** to the `target`.
Return the **sum** (not the triplet).

---

### 🔍 Example

```python
Input:  nums = [-1, 2, 1, -4], target = 1
Output: 2
```

**Explanation:**
All possible triplets are:

| Triplet     | Sum | Distance from target (1) |
| ----------- | --- | ------------------------ |
| (-1, 2, 1)  | 2   | 1                        |
| (-1, 2, -4) | -3  | 4                        |
| (-1, 1, -4) | -4  | 5                        |
| (2, 1, -4)  | -1  | 2                        |

The closest sum to `1` is `2` → ✅ output = **2**

---

## ⚙️ 2. Example Visualization

```
nums = [-1, 2, 1, -4]
target = 1
```

We need 3 numbers that add up closest to 1.

* (-1 + 2 + 1) = 2 → difference = |2 - 1| = 1 ✅
* (-1 + 2 + -4) = -3 → diff = 4
* (-1 + 1 + -4) = -4 → diff = 5
* (2 + 1 + -4) = -1 → diff = 2

**Answer = 2**

---

## 🧩 3. Approach 1 — Brute Force (Three Loops)

This is the most direct approach.

### 💡 **Idea**

1. Use **three nested loops** (`i`, `j`, `k`) to generate all possible triplets.
2. For each triplet, calculate its sum.
3. Track the one that’s *closest* to the target (smallest absolute difference).

---

### ⏱️ Time Complexity: O(n³)

You try every combination of three numbers.

### 💾 Space Complexity: O(1)

We only store the best sum found.

---

### 🧾 Code — Brute Force

```python
class Solution:
    def threeSumClosest(self, nums: list[int], target: int) -> int:
        n = len(nums)
        closest_sum = float('inf')  # Start with infinity
        
        for i in range(n - 2):
            for j in range(i + 1, n - 1):
                for k in range(j + 1, n):
                    current_sum = nums[i] + nums[j] + nums[k]
                    
                    # Update if closer to target
                    if abs(target - current_sum) < abs(target - closest_sum):
                        closest_sum = current_sum
                        
        return closest_sum
```

---

## 🧠 Code Line in Context

```python
if abs(target - current_sum) < abs(target - closest_sum):
    closest_sum = current_sum
```

---

## 🧩 Meaning in Simple Words

* `target` = what we want to get close to.
* `current_sum` = the sum of the current 3 numbers (triplet).
* `closest_sum` = the best (closest) sum we’ve found so far.

We **compare** how far each sum is from the target using `abs()` (absolute value).

👉 The one that has a **smaller difference** is **closer** to the target.

---

## ⚙️ Step-by-Step Logic

| Variable                    | Meaning                                       |
| --------------------------- | --------------------------------------------- |
| `abs(target - current_sum)` | Distance of current triplet’s sum from target |
| `abs(target - closest_sum)` | Distance of best-known sum so far from target |
| `if <`                      | If the current sum is closer than before      |
| `closest_sum = current_sum` | Update the “best so far”                      |

---

## 🧮 Example: Full Dry Run

Let’s take:

```python
nums = [-1, 2, 1, -4]
target = 1
```

All triplets (using `itertools.combinations(nums, 3)`):

| Triplet     | Sum | `abs(target - current_sum)` | Compare vs current `closest_sum` | Action                           |
| ----------- | --- | --------------------------- | -------------------------------- | -------------------------------- |
| (-1, 2, 1)  | 2   | `abs(1 - 2)` = **1**        | `abs(1 - inf)` = inf             | ✅ Update → `closest_sum = 2`     |
| (-1, 2, -4) | -3  | `abs(1 - (-3))` = **4**     | `abs(1 - 2)` = 1                 | ❌ 4 > 1 → Keep `closest_sum = 2` |
| (-1, 1, -4) | -4  | `abs(1 - (-4))` = **5**     | `abs(1 - 2)` = 1                 | ❌ 5 > 1 → Keep `closest_sum = 2` |
| (2, 1, -4)  | -1  | `abs(1 - (-1))` = **2**     | `abs(1 - 2)` = 1                 | ❌ 2 > 1 → Keep `closest_sum = 2` |

✅ **Final `closest_sum = 2`**




✅ Simple logic.
❌ But **too slow** (O(n³)) for large arrays.

---

## 🧩 4. Approach 2 — Two Pointers (Optimal)

This is the efficient and elegant version (O(n²)).

### 💡 **Core Idea**

It’s based on the **3Sum** pattern — sort the array, fix one number, and use two pointers to find the best combination for the remaining two.

---

### 🧠 Step-by-Step Logic

1. Sort the array first → this allows two-pointer traversal.
2. Fix the first number `nums[i]`.
3. Use two pointers:

   * `left = i + 1`
   * `right = len(nums) - 1`
4. Calculate the current sum = `nums[i] + nums[left] + nums[right]`.
5. If it’s closer to target than the best we’ve seen, **update** it.
6. Move pointers:

   * If `current_sum < target` → need a bigger sum → move `left += 1`
   * If `current_sum > target` → need a smaller sum → move `right -= 1`
   * If `current_sum == target` → perfect match, return it immediately.
7. Continue until `left >= right`.

---

### 💡 Intuition

Sorting + two-pointer technique reduces search space:

* Each fixed `i` only needs a **linear scan** for the best pair.
* Avoids redundant combinations.

---

## 🧾 5. Full Code with Comments (Optimal)

```python
class Solution:
    def threeSumClosest(self, nums: list[int], target: int) -> int:
        nums.sort()  # Sort array for two-pointer traversal
        n = len(nums)
        
        closest_sum = float('inf')  # Store the best (closest) sum
        
        # Fix one number at a time
        for i in range(n - 2):
            left, right = i + 1, n - 1
            
            while left < right:
                current_sum = nums[i] + nums[left] + nums[right]
                
                # If current_sum is closer to target, update it
                if abs(target - current_sum) < abs(target - closest_sum):
                    closest_sum = current_sum
                
                # Move pointers based on comparison
                if current_sum < target:
                    left += 1   # We need a larger sum
                elif current_sum > target:
                    right -= 1  # We need a smaller sum
                else:
                    # Perfect match found
                    return current_sum
                    
        return closest_sum
```

---

## 🧮 6. Dry Run (Step-by-Step)

**Input:**

```python
nums = [-1, 2, 1, -4]
target = 1
```

### Step 1: Sort

`nums = [-4, -1, 1, 2]`

### Step 2: Initialize

`closest_sum = inf`

---

### Loop 1: i = 0 → nums[i] = -4

`left = 1`, `right = 3`

| left | right | Triplet     | Sum | Diff | Action                             |
| ---- | ----- | ----------- | --- | ---- | ---------------------------------- |
| -1   | 2     | (-4, -1, 2) | -3  | 4    | closer → update `closest_sum = -3` |
| 1    | 2     | (-4, 1, 2)  | -1  | 2    | closer → update `closest_sum = -1` |

Now `left` moves to `2`, `right` becomes `2` → stop loop.

---

### Loop 2: i = 1 → nums[i] = -1

`left = 2`, `right = 3`

| left | right | Triplet    | Sum | Diff | Action                            |
| ---- | ----- | ---------- | --- | ---- | --------------------------------- |
| 1    | 2     | (-1, 1, 2) | 2   | 1    | closer → update `closest_sum = 2` |

✅ Perfect: `2` is closest to `1`.

Loop ends.

---

**Final Answer → `2`**

---

## 📊 7. Time & Space Analysis

| Approach    | Time  | Space | Comments                |
| ----------- | ----- | ----- | ----------------------- |
| Brute Force | O(n³) | O(1)  | Every triplet           |
| Two Pointer | O(n²) | O(1)  | Efficient, sorted array |

---

## 🧪 8. Quick Test Cases

```python
sol = Solution()

# Example 1
print(sol.threeSumClosest([-1, 2, 1, -4], 1))
# ✅ Output: 2

# Example 2
print(sol.threeSumClosest([0, 0, 0], 1))
# ✅ Output: 0 (only one possible sum)

# Example 3
print(sol.threeSumClosest([1, 1, 1, 0], 100))
# ✅ Output: 3 (closest we can get)

# Example 4
print(sol.threeSumClosest([-3, -2, -5, 3, -4], -1))
# ✅ Output: -2
```

---

## 🧠 9. Summary Comparison

| Approach        | Description                                 | Time  | Space | Suitable for                       |
| --------------- | ------------------------------------------- | ----- | ----- | ---------------------------------- |
| **Brute Force** | Try every triplet, check closeness manually | O(n³) | O(1)  | Understanding logic                |
| **Two Pointer** | Sort + fix one + move two inward            | O(n²) | O(1)  | ✅ Best for interview / performance |

---

✅ **Final Takeaway**

* Brute Force → good for understanding.
* Two Pointers → optimal in both speed and simplicity.
* Always remember:

  * Sort array first.
  * Fix one number.
  * Adjust pointers intelligently.
  * Update only when closer.

---
