---

# 🧩 LeetCode 80 — Remove Duplicates from Sorted Array II

We’ll cover:

1️⃣ Problem Understanding
2️⃣ Example Explanation
3️⃣ Approach 1 — Brute Force (Using Extra Space)
4️⃣ Approach 2 — Two Pointer (Optimal, In-Place)
5️⃣ Full Code with Comments
6️⃣ Dry Run (Step-by-Step for Both Approaches)
7️⃣ Time & Space Analysis
8️⃣ Quick Test Cases
9️⃣ Summary Comparison

---

## 🧠 1. Problem Understanding (Simplified)

We are given a **sorted array** `nums` (non-decreasing order).
We must **remove duplicates in-place**, but this time —
➡️ each element can appear **at most twice**.

We must return:

* `k` → the number of valid elements (first `k` positions will be correct).
* Modify the array **in-place**.

Elements beyond `k` can be ignored.

---

### ⚙️ Example 1

**Input:**
`nums = [1,1,1,2,2,3]`
**Output:**
`k = 5, nums = [1,1,2,2,3,_]`

**Explanation:**

* `1` appears 3 times → keep 2
* `2` appears 2 times → keep both
* `3` appears 1 time → keep it

---

### ⚙️ Example 2

**Input:**
`nums = [0,0,1,1,1,1,2,3,3]`
**Output:**
`k = 7, nums = [0,0,1,1,2,3,3,_,_]`

---

### ⚙️ Constraints

```
1 <= nums.length <= 3 * 10^4
-10^4 <= nums[i] <= 10^4
nums is sorted in non-decreasing order
```

---

## 🧩 2. Approach 1 — Brute Force (Using Extra Space)

### 💡 Idea

We can count how many times each number appears using a dictionary (or Counter),
then rebuild the array keeping each element **up to 2 times**.

---

### ⏱️ Time Complexity: O(n)

### 💾 Space Complexity: O(n)

### ✅ Simplicity: Easy to understand, but **not in-place**

---

### 🧾 Code — Brute Force

```python
from collections import Counter

class Solution:
    def removeDuplicates(self, nums: list[int]) -> int:
        count = Counter(nums)
        result = []

        # Collect elements up to twice
        for num in nums:
            if count[num] > 0:
                allowed = min(2, count[num])
                result.extend([num] * allowed)
                count[num] = 0  # avoid re-adding
        
        # Copy result back to nums
        k = len(result)
        for i in range(k):
            nums[i] = result[i]
        return k
```

---


✅ **Final Output:**

```
nums = [1,1,2,2,3,_]
k = 5
```
# 🧩 Step-by-Step Dry Run (Approach 1 — Brute Force)

### Input:

`nums = [1, 1, 1, 2, 2, 3]`

---

### Initial State

We create a Counter to store occurrences.
`count = {1: 3, 2: 2, 3: 1}`
`result = []`

We’ll iterate through each number and pick at most 2 copies.

---

**Loop 1: num = 1**
Check → `count[1] = 3` → greater than 0 ✅
Allowed copies = `min(2, 3) = 2`
Action → Add two 1’s → `[1, 1]`
Update `count[1] = 0`

---

**Loop 2: num = 1 (next one)**
Check → `count[1] = 0` → ❌ skip (already added)
Action → Nothing happens
`result = [1, 1]`

---

**Loop 3: num = 1 (again)**
Still `count[1] = 0` → ❌ skip
`result = [1, 1]`

---

**Loop 4: num = 2**
Check → `count[2] = 2` → ✅ allowed = `min(2, 2) = 2`
Action → Add two 2’s → `[1, 1, 2, 2]`
Update `count[2] = 0`

---

**Loop 5: num = 2 (next one)**
Check → `count[2] = 0` → ❌ skip
`result = [1, 1, 2, 2]`

---

**Loop 6: num = 3**
Check → `count[3] = 1` → ✅ allowed = `min(2, 1) = 1`
Action → Add one 3 → `[1, 1, 2, 2, 3]`
Update `count[3] = 0`

---

**End of Loop**

✅ Final `result = [1, 1, 2, 2, 3]`
✅ Copy back to original array: `nums = [1, 1, 2, 2, 3, _]`
✅ Return `k = len(result) = 5`

---
---

## 🧩 3. Approach 2 — Two Pointer (Optimal, In-Place)

### 💡 Idea

Since `nums` is sorted, all duplicates are **next to each other**.
We only need to **allow at most 2 occurrences** of each number.

We’ll use the **two-pointer technique** again:

* `i` → position of next valid element
* `j` → scans all elements

---

### 🧠 Logic

Start with:

* `i = 2` (since the first two elements are always valid)
* Iterate `j` from 2 to end

If current element `nums[j]` ≠ `nums[i - 2]`,
it means `nums[j]` is valid (it doesn’t exceed 2 occurrences).
Copy it to `nums[i]`, and increment `i`.

---

| Pointer | Meaning                   |
| ------- | ------------------------- |
| `i`     | Next valid write position |
| `j`     | Current scanning index    |

---

### ⏱️ Time Complexity: O(n)

### 💾 Space Complexity: O(1)

✅ In-place & Optimal

---

### 🧾 Code — Two Pointer (Optimal)

```python
class Solution:
    def removeDuplicates(self, nums: list[int]) -> int:
        if len(nums) <= 2:
            return len(nums)

        i = 2  # first two always allowed
        for j in range(2, len(nums)):
            if nums[j] != nums[i - 2]:
                nums[i] = nums[j]
                i += 1
        return i
```





# 🧩 Step-by-Step Dry Run (Approach 2 — Two Pointer, In-Place)

### Input:

`nums = [1, 1, 1, 2, 2, 3]`

---

### Initial State

We know the first 2 elements are always valid.
So, we start from index **i = 2**, and loop with **j** starting from 2.

```
[ 1, 1, 1, 2, 2, 3 ]
      ↑
      j
      ↑
      i
```

---

### Loop 1: j = 2

Pointers: i = 2, j = 2
Check: `nums[j] != nums[i - 2]`
Values: `nums[2] = 1`, `nums[0] = 1`
Condition: `1 != 1 → False`
Result: ❌ Too many duplicates
Action: Nothing happens

Array stays same: `[1, 1, 1, 2, 2, 3]`

---

### Loop 2: j = 3

Pointers: i = 2, j = 3
Check: `nums[j] != nums[i - 2]`
Values: `nums[3] = 2`, `nums[0] = 1`
Condition: `2 != 1 → True ✅`
Action:

* Place `nums[j]` at `nums[i]` → `nums[2] = 2`
* Increment i → `i = 3`

Array becomes:
`[1, 1, 2, 2, 2, 3]`

```
[ 1, 1, 2, 2, 2, 3 ]
         ↑
         i
            ↑
            j
```

---

### Loop 3: j = 4

Pointers: i = 3, j = 4
Check: `nums[j] != nums[i - 2]`
Values: `nums[4] = 2`, `nums[1] = 1`
Condition: `2 != 1 → True ✅`
Action:

* Place `nums[j]` at `nums[i]` → `nums[3] = 2`
* Increment i → `i = 4`

Array becomes:
`[1, 1, 2, 2, 2, 3]`

```
[ 1, 1, 2, 2, 2, 3 ]
            ↑
            i
               ↑
               j
```

---

### Loop 4: j = 5

Pointers: i = 4, j = 5
Check: `nums[j] != nums[i - 2]`
Values: `nums[5] = 3`, `nums[2] = 2`
Condition: `3 != 2 → True ✅`
Action:

* Place `nums[j]` at `nums[i]` → `nums[4] = 3`
* Increment i → `i = 5`

Array becomes:
`[1, 1, 2, 2, 3, 3]`

```
[ 1, 1, 2, 2, 3, 3 ]
               ↑
               i
                  ↑
                  j
```

---

### End of Loop

✅ j has reached the end
✅ `i = 5`

**Return Value:**
`i = 5` → `k = 5`
**Final Array:** `[1, 1, 2, 2, 3, _]`

---



---

## ⚡ 7. Time & Space Analysis

| Metric                    | Brute Force | Two Pointer (Optimal) |
| ------------------------- | ----------- | --------------------- |
| **Time Complexity**       | O(n)        | O(n)                  |
| **Space Complexity**      | O(n)        | O(1)                  |
| **In-Place?**             | ❌ No        | ✅ Yes                 |
| **Ease of Understanding** | ✅ Easy      | ⚡ Moderate            |
| **LeetCode Preferred**    | ❌ No        | ✅ Yes                 |

---

## 🧪 8. Quick Test Cases

```python
nums = [1,1,1,2,2,3]
print(Solution().removeDuplicates(nums), nums)
# ➜ 5 [1,1,2,2,3,_]

nums = [0,0,1,1,1,1,2,3,3]
print(Solution().removeDuplicates(nums), nums)
# ➜ 7 [0,0,1,1,2,3,3,_,_]

nums = [1,2,3]
print(Solution().removeDuplicates(nums), nums)
# ➜ 3 [1,2,3]

nums = [1,1]
print(Solution().removeDuplicates(nums), nums)
# ➜ 2 [1,1]
```

---

## 🧠 9. Summary Comparison

| Approach           | Description                      | Time | Space | Best Use Case                       |
| ------------------ | -------------------------------- | ---- | ----- | ----------------------------------- |
| **1. Brute Force** | Use Counter, rebuild array       | O(n) | O(n)  | Simple, easy to code                |
| **2. Two Pointer** | In-place overwrite (≤ 2 allowed) | O(n) | O(1)  | ✅ Optimal for interviews & LeetCode |

---

### 🔑 Key Takeaway

> This problem extends **LeetCode #26** by allowing each number up to **two occurrences**.
> The key trick:
>
> ```python
> if nums[j] != nums[i - 2]:
>     nums[i] = nums[j]
>     i += 1
> ```
>
> ensures we never allow more than 2 of the same element while keeping it in-place.

---

Would you like me to now turn this into a **GitHub-ready Markdown note** (with badges, collapsible “Dry Run” sections, and formatted headers like your previous notes)?
