

# 🧩 **LeetCode 26 — Remove Duplicates from Sorted Array**

in the **exact same detailed format** you loved for “Valid Palindrome.”

We’ll cover:

1️⃣ Problem Understanding
2️⃣ Example Explanation
3️⃣ Approach 1 — Brute Force (Using Extra Space)
4️⃣ Approach 2 — Two Pointer (Optimal, In-Place)
5️⃣ Full Code with Comments
6️⃣ Dry Run (Step-by-Step Table)
7️⃣ Time & Space Analysis
8️⃣ Quick Test Cases
9️⃣ Summary Comparison

---

## 🧠 1. Problem Understanding (Simplified)

We are given a **sorted array** `nums` (in non-decreasing order).
We must **remove duplicates in-place** so that:

* Each element appears **only once**
* The **relative order** of elements is preserved

Return the **number `k`** — the count of unique elements.

After the function runs, the first `k` elements of `nums` should contain the **unique numbers** in sorted order.

---

### ⚙️ Example 1

```python
Input:  nums = [1,1,2]
Output: k = 2, nums = [1,2,_]
```

**Explanation:**

* Unique elements = [1,2]
* `_` means any leftover value beyond k is ignored.

---

### ⚙️ Example 2

```python
Input:  nums = [0,0,1,1,1,2,2,3,3,4]
Output: k = 5, nums = [0,1,2,3,4,_,_,_,_,_]
```

**Explanation:**
Unique part → `[0,1,2,3,4]`

---

### ⚙️ Constraints

```
1 <= nums.length <= 3 * 10^4
-100 <= nums[i] <= 100
nums is sorted in non-decreasing order
```

---

## 🧩 2. Approach 1 — Brute Force (Using Extra Space)

---

### 💡 **Idea**

1. Use a **set** to store unique numbers.
2. Convert back to sorted list.
3. Copy them to the original array.

❌ But this **doesn’t modify in-place efficiently** (extra O(n) space).

---

### ⏱️ Time Complexity: O(n)

### 💾 Space Complexity: O(n)

---

### 🧾 Code — Brute Force

```python
class Solution:
    def removeDuplicates(self, nums: list[int]) -> int:
        unique = sorted(set(nums))  # store unique and sort
        k = len(unique)

        # copy back to nums
        for i in range(k):
            nums[i] = unique[i]
        return k
```

✅ Easy, but **not the optimal in-place approach** LeetCode expects.

---

## 🧩 3. Approach 2 — Two Pointer (Optimal, In-Place)

---

### 💡 **Idea**

Since the array is **sorted**,
→ duplicates will always be **next to each other**.

We can use **two pointers**:

| Pointer | Meaning                                |
| ------- | -------------------------------------- |
| `i`     | tracks the last unique element’s index |
| `j`     | scans through the array                |

---

### 🧠 Logic

1. Start with `i = 0` (first element always unique).
2. Iterate `j` from `1` to `len(nums)-1`:

   * If `nums[j] != nums[i]`, it means a new unique element found!
     → Move `i` ahead and copy it: `nums[i] = nums[j]`
3. Finally, number of unique elements = `i + 1`

---

### ⏱️ **Time Complexity:** O(n)

### 💾 **Space Complexity:** O(1) — done in-place

---

### 🧾 **Code — Two Pointer**

```python
class Solution:
    def removeDuplicates(self, nums: list[int]) -> int:
        if not nums:
            return 0

        # i -> position of last unique element
        i = 0

        # j -> scanning pointer
        for j in range(1, len(nums)):
            # When new unique element found
            if nums[j] != nums[i]:
                i += 1
                nums[i] = nums[j]  # place it next

        # Number of unique elements
        return i + 1
```

---

## 🧮 **Dry Run — Example: `nums = [0,0,1,1,1,2,2,3,3,4]`**

| Step | i | j | nums[i] | nums[j] | Condition (nums[j] != nums[i]) | Action         | nums (after step)     |
| ---- | - | - | ------- | ------- | ------------------------------ | -------------- | --------------------- |
| 1    | 0 | 1 | 0       | 0       | ❌ same                         | —              | [0,0,1,1,1,2,2,3,3,4] |
| 2    | 0 | 2 | 0       | 1       | ✅ diff                         | i=1; nums[1]=1 | [0,1,1,1,1,2,2,3,3,4] |
| 3    | 1 | 3 | 1       | 1       | ❌ same                         | —              | [0,1,1,1,1,2,2,3,3,4] |
| 4    | 1 | 4 | 1       | 1       | ❌ same                         | —              | [0,1,1,1,1,2,2,3,3,4] |
| 5    | 1 | 5 | 1       | 2       | ✅ diff                         | i=2; nums[2]=2 | [0,1,2,1,1,2,2,3,3,4] |
| 6    | 2 | 6 | 2       | 2       | ❌ same                         | —              | [0,1,2,1,1,2,2,3,3,4] |
| 7    | 2 | 7 | 2       | 3       | ✅ diff                         | i=3; nums[3]=3 | [0,1,2,3,1,2,2,3,3,4] |
| 8    | 3 | 8 | 3       | 3       | ❌ same                         | —              | [0,1,2,3,1,2,2,3,3,4] |
| 9    | 3 | 9 | 3       | 4       | ✅ diff                         | i=4; nums[4]=4 | [0,1,2,3,4,2,2,3,3,4] |

---

✅ End of loop:

```
i = 4
Unique count = i + 1 = 5
nums = [0,1,2,3,4,_,_,_,_,_]
```

---

### ✅ **Answer**

```
Return k = 5
Modified nums = [0,1,2,3,4,_,_,_,_,_]
```

---

## 🧩 4. Quick Test Cases

```python
sol = Solution()

nums1 = [1,1,2]
print(sol.removeDuplicates(nums1), nums1)  # ✅ 2, [1,2,_]

nums2 = [0,0,1,1,1,2,2,3,3,4]
print(sol.removeDuplicates(nums2), nums2)  # ✅ 5, [0,1,2,3,4,_,_,_,_,_]

nums3 = [1,2,3]
print(sol.removeDuplicates(nums3), nums3)  # ✅ 3, [1,2,3]

nums4 = [1,1,1,1]
print(sol.removeDuplicates(nums4), nums4)  # ✅ 1, [1,_,_,_]
```

---

## 🏁 Output

```
2 [1, 2, 2]
5 [0, 1, 2, 3, 4, 2, 2, 3, 3, 4]
3 [1, 2, 3]
1 [1, 1, 1, 1]
```

---

## 🧠 Summary Comparison

| Approach           | Description                       | Time | Space | Best Use Case        |
| ------------------ | --------------------------------- | ---- | ----- | -------------------- |
| **1. Brute Force** | Use set() to get unique values    | O(n) | O(n)  | Simple, not in-place |
| **2. Two Pointer** | In-place overwrite while scanning | O(n) | O(1)  | Optimal, accepted    |

---



