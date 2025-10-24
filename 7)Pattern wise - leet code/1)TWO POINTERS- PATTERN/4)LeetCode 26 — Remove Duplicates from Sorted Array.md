

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

-----

# Dry Run: Remove Duplicates (Two-Pointer Method)

-----

This document explains the "fast/slow" pointer (or "Gatekeeper/Explorer") technique for solving LeetCode \#26: Remove Duplicates from Sorted Array.

The process is like "compacting" the array in place.

## The Pointers' Jobs

Think of the two pointers, `i` and `j`, as having different jobs:

  * **`i` (The Slow Pointer / Gatekeeper) 📝**

      * `i` points to the last unique element that has been *placed* in the "good" section of the array.
      * It **only moves** when a new unique number is found.

  * **`j` (The Fast Pointer / Explorer) 🕵️**

      * `j` moves forward one step at a time to **explore every element** in the array.

The core logic is this line. It's the "Gatekeeper" (`i`) saying to the "Explorer" (`j`): "You found a new unique item\! I will copy it into the empty slot right after me."

```python
if nums[j] != nums[i]:
    i += 1
    nums[i] = nums[j]
```

## Step-by-Step Dry Run

Let's trace the algorithm with this example.

**Input:** `nums = [0, 0, 1, 1, 2]`

### Initial State

The `for` loop starts `j` at index 1. `i` starts at 0.

  * `i = 0`
  * `j` is not yet in the loop.

<!-- end list -->

```bash
[ 0, 0, 1, 1, 2 ]
  i
```

-----

### Inside the Loop

  * **Loop 1: `j = 1`**

      * **Pointers:** `i = 0`, `j = 1`
      * **Array:**
        ```bash
        [ 0, 0, 1, 1, 2 ]
          i  j
        ```
      * **Check:** `if nums[j] != nums[i]`
      * **Values:** `if 0 != 0`
      * **Result:** `False` (It's a duplicate).
      * **Action:** Nothing happens.

  * **Loop 2: `j = 2`**

      * **Pointers:** `i = 0`, `j = 2`
      * **Array:**
        ```bash
        [ 0, 0, 1, 1, 2 ]
          i     j
        ```
      * **Check:** `if nums[j] != nums[i]`
      * **Values:** `if 1 != 0`
      * **Result:** `True` (We found a new unique element\!)
      * **Action:**
        1.  `i += 1` (Now `i = 1`)
        2.  `nums[i] = nums[j]`
              * `nums[1] = nums[2]`
              * `nums[1] = 1`
      * **Array is now:** `[ 0, 1, 1, 1, 2 ]` (The `1` from `nums[2]` **overwrites** the `0` at `nums[1]`)
        ```bash
        [ 0, 1, 1, 1, 2 ]
             i  j
        ```

  * **Loop 3: `j = 3`**

      * **Pointers:** `i = 1`, `j = 3`
      * **Array:**
        ```bash
        [ 0, 1, 1, 1, 2 ]
             i     j
        ```
      * **Check:** `if nums[j] != nums[i]`
      * **Values:** `if 1 != 1`
      * **Result:** `False` (It's a duplicate of the *newest* unique number).
      * **Action:** Nothing happens.

  * **Loop 4: `j = 4`**

      * **Pointers:** `i = 1`, `j = 4`
      * **Array:**
        ```bash
        [ 0, 1, 1, 1, 2 ]
             i        j
        ```
      * **Check:** `if nums[j] != nums[i]`
      * **Values:** `if 2 != 1`
      * **Result:** `True` (We found another new unique element\!)
      * **Action:**
        1.  `i += 1` (Now `i = 2`)
        2.  `nums[i] = nums[j]`
              * `nums[2] = nums[4]`
              * `nums[2] = 2`
      * **Array is now:** `[ 0, 1, 2, 1, 2 ]` (The `2` from `nums[4]` **overwrites** the `1` at `nums[2]`)
        ```bash
        [ 0, 1, 2, 1, 2 ]
                i     j
        ```

-----

## End of Loop

  * `j` has reached the end of the array. The loop stops.
  * **Final Array:** `[ 0, 1, 2, 1, 2 ]`
  * **Return Value:** The function returns `i + 1`, which is `2 + 1 = 3`.


---

## 🧠 Summary Comparison

| Approach           | Description                       | Time | Space | Best Use Case        |
| ------------------ | --------------------------------- | ---- | ----- | -------------------- |
| **1. Brute Force** | Use set() to get unique values    | O(n) | O(n)  | Simple, not in-place |
| **2. Two Pointer** | In-place overwrite while scanning | O(n) | O(1)  | Optimal, accepted    |

---



