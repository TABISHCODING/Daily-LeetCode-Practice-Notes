

-----

# 🧩 **LeetCode 88 — Merge Sorted Array**

This is a classic interview problem that seems simple but has a very clever optimal solution to meet the **in-place** constraint. It's a perfect example of the **Two Pointer (Opposite Direction)** pattern, but in a modified way.

We’ll cover:

1.  Problem Understanding
2.  Example Explanation
3.  Approach 1 — Brute Force (Create New, Sort, Copy Back)
4.  Approach 2 — Three Pointers (Optimal, In-Place from Back)
5.  Full Code with Comments (Optimal)
6.  Dry Run (Step-by-Step Visual)
7.  Time & Space Analysis
8.  Quick Test Cases
9.  Summary Comparison

-----

## 🧠 1. Problem Understanding (Simplified)

We are given **two** sorted arrays:

1.  `nums1`: A large array of size `m + n`. The first `m` elements are the real, sorted data. The last `n` elements are just `0`s, acting as empty padding.
2.  `nums2`: A smaller array of size `n` containing its own sorted data.

Our goal is to **merge `nums2` into `nums1`** to create one single, sorted array.

**The catch:** We must modify `nums1` **in-place**. We cannot create a new array to return.

-----

## ⚙️ 2. Example Explanation

### ⚙️ Example 1

```python
Input:
nums1 = [1, 2, 3, 0, 0, 0], m = 3
nums2 = [2, 5, 6], n = 3

Output: nums1 = [1, 2, 2, 3, 5, 6]
```

**Explanation:**

  * The "real" part of `nums1` is `[1, 2, 3]`.
  * The `nums2` array is `[2, 5, 6]`.
  * The function merges these two lists into the `nums1` array, resulting in `[1, 2, 2, 3, 5, 6]`. The `0`s are completely overwritten.

-----

## 🧩 3. Approach 1 — Brute Force (Create New, Sort, Copy Back)

This is a clear, straightforward approach that you proposed. Instead of trying to be "in-place," it uses extra memory to make the logic simple.

### 💡 **Idea**

1.  Create a **new list** called `merged`.
2.  Fill this new list with the *valid* elements from `nums1` (using the slice `nums1[:m]`) and all elements from `nums2` (using `nums2[:n]`).
3.  Sort this new `merged` list using `.sort()`.
4.  Copy all the sorted elements from `merged` back into the original `nums1` array, overwriting everything from the beginning.

-----

### ⏱️ Time Complexity: $O((m+n) \log(m+n))$

The dominant operation is `merged.sort()`. Sorting an array of size $k$ takes $O(k \log k)$ time. Our `merged` list is size $m+n$, so the time is $O((m+n) \log(m+n))$.

### 💾 Space Complexity: $O(m+n)$

We create a new list `merged` that holds $m+n$ elements. This explicitly uses $O(m+n)$ extra space, which violates the "in-place" requirement.

-----

### 🧾 Code — Brute Force

```python
class Solution:
    def merge(self, nums1: list[int], m: int, nums2: list[int], n: int) -> None:
        
        # 1. Create a new list with the valid parts of nums1 and nums2
        merged = nums1[:m] + nums2[:n]
        
        # 2. Sort the new list
        merged.sort()
        
        # 3. Copy the sorted list back into nums1
        for i in range(m + n):
            nums1[i] = merged[i]
```

✅ Very clear, readable, and "Pythonic."
❌ **Fails the $O(1)$ space (in-place) constraint.**

-----

## 🧩 4. Approach 2 — Three Pointers (Optimal, In-Place from Back)

This is the clever, optimal solution.

### 💡 **Idea**

If we try to merge from the **front** (index `0`), we'll overwrite the data in `nums1` that we still need to check (e.g., `nums1 = [4, 5, 0]` and `nums2 = [1]`. If we put `1` at `nums1[0]`, we lose the `4`).

**The Key Insight:** Since the empty space is at the **end** of `nums1`, we should fill it from the end\! We will merge the arrays **in reverse**, placing the *largest* elements first.

| Pointer | Meaning (Job) |
| :--- | :--- |
| `p1` | **`nums1` pointer** 📝<br>Starts at the end of the *real* data in `nums1` (at index `m - 1`). |
| `p2` | **`nums2` pointer** 🕵️<br>Starts at the end of `nums2` (at index `n - 1`). |
| `p_write`| **Write Pointer** ✍️<br>Starts at the very end of `nums1` (at index `m + n - 1`). This is where we'll write the largest value. |

-----

### 🧠 Logic

1.  Initialize the three pointers: `p1 = m - 1`, `p2 = n - 1`, `p_write = m + n - 1`.
2.  Loop `while p1 >= 0` AND `p2 >= 0` (while both arrays still have elements to check).
3.  Compare `nums1[p1]` and `nums2[p2]`.
      * **If `nums1[p1]` is larger:** Copy its value to `nums1[p_write]`. Then, decrement `p1` (to check the next-smallest `nums1` item).
      * **If `nums2[p2]` is larger (or equal):** Copy *its* value to `nums1[p_write]`. Then, decrement `p2`.
4.  No matter which one we picked, we *always* decrement `p_write` because we just filled that slot.
5.  **Cleanup:** After the main loop, `p1` or `p2` (or both) might be `< 0`.
      * If `p1` is still `> 0`, it means `nums1` has leftover small elements. We don't need to do anything\! They are *already* in their correct sorted positions at the front of `nums1`.
      * If `p2` is still `> 0`, it means `nums2` has leftover small elements (e.g., `nums1 = [4, 5, 0, 0]` and `nums2 = [1, 2]`). We must copy these remaining elements into the front of `nums1`. We can do this with a `while p2 >= 0` loop.

-----

## 🧾 5. Full Code with Comments (Optimal)

```python
class Solution:
    def merge(self, nums1: list[int], m: int, nums2: list[int], n: int) -> None:
        """
        Do not return anything, modify nums in-place.
        """
        
        # 1. Initialize pointers
        # Pointer for last real element in nums1
        p1 = m - 1
        # Pointer for last element in nums2
        p2 = n - 1
        # Pointer for the slot to write into (very end of nums1)
        p_write = m + n - 1
        
        # 2. Main merge loop (runs as long as both arrays have items)
        while p1 >= 0 and p2 >= 0:
            if nums1[p1] > nums2[p2]:
                # nums1's item is bigger, place it at the end
                nums1[p_write] = nums1[p1]
                p1 -= 1
            else:
                # nums2's item is bigger (or equal), place it at the end
                nums1[p_write] = nums2[p2]
                p2 -= 1
            
            # Move the write-pointer one step to the left
            p_write -= 1
            
        # 3. Cleanup loop
        # If nums2 still has items left, they must be the smallest.
        # Copy them into the remaining slots at the front of nums1.
        # (We don't need a `while p1 >= 0` loop, because those
        # items are already in the correct place.)
        while p2 >= 0:
            nums1[p_write] = nums2[p2]
            p2 -= 1
            p_write -= 1
```

-----

## 🧮 6. Dry Run (Step-by-Step Visual)

Here is a dry run for the "Merge from Back" algorithm.

### The Pointers' Jobs

  * **`p1` (Pointer 1) 📝:** Points to the largest *un-merged* item in `nums1`.
  * **`p2` (Pointer 2) 🕵️:** Points to the largest *un-merged* item in `nums2`.
  * **`p_write` (Write Pointer) ✍️:** Points to the next *empty slot* in `nums1` (working from back to front).

### Dry Run Example

Let's use `nums1 = [1, 2, 3, 0, 0, 0]`, `m = 3`, `nums2 = [2, 5, 6]`, `n = 3`

**Initial State:**

  * `p1 = 3 - 1 = 2` (points to `3`)
  * `p2 = 3 - 1 = 2` (points to `6`)
  * `p_write = 3 + 3 - 1 = 5` (points to the last `0`)

`nums1 = [ 1, 2, 3, 0, 0, 0 ]`
                                `p1`                        `p_write`
`nums2 = [ 2, 5, 6 ]`
                                `p2`

-----

**Loop 1:**

  * **Pointers:** `p1 = 2`, `p2 = 2`, `p_write = 5`
  * **Check:** `if nums1[2] > nums2[2]`
  * **Values:** `if 3 > 6`
  * **Result:** `False`. (The `else` block runs).
  * **Action:**
    1.  `nums1[p_write] = nums2[p2]` → `nums1[5] = 6`
    2.  `p2 -= 1` (Now `p2 = 1`)
    3.  `p_write -= 1` (Now `p_write = 4`)
  * **`nums1` is now:** `[ 1, 2, 3, 0, 0, 6 ]`
                                    `p1`              `p_write`

-----

**Loop 2:**

  * **Pointers:** `p1 = 2`, `p2 = 1`, `p_write = 4`
  * **Check:** `if nums1[2] > nums2[1]`
  * **Values:** `if 3 > 5`
  * **Result:** `False`. (The `else` block runs).
  * **Action:**
    1.  `nums1[p_write] = nums2[p2]` → `nums1[4] = 5`
    2.  `p2 -= 1` (Now `p2 = 0`)
    3.  `p_write -= 1` (Now `p_write = 3`)
  * **`nums1` is now:** `[ 1, 2, 3, 0, 5, 6 ]`
                                    `p1`        `p_write`

-----

**Loop 3:**

  * **Pointers:** `p1 = 2`, `p2 = 0`, `p_write = 3`
  * **Check:** `if nums1[2] > nums2[0]`
  * **Values:** `if 3 > 2`
  * **Result:** `True`. (The `if` block runs).
  * **Action:**
    1.  `nums1[p_write] = nums1[p1]` → `nums1[3] = 3`
    2.  `p1 -= 1` (Now `p1 = 1`)
    3.  `p_write -= 1` (Now `p_write = 2`)
  * **`nums1` is now:** `[ 1, 2, 3, 3, 5, 6 ]`
                            `p1` `p_write`

-----

**Loop 4:**

  * **Pointers:** `p1 = 1`, `p2 = 0`, `p_write = 2`
  * **Check:** `if nums1[1] > nums2[0]`
  * **Values:** `if 2 > 2`
  * **Result:** `False`. (The `else` block runs).
  * **Action:**
    1.  `nums1[p_write] = nums2[p2]` → `nums1[2] = 2`
    2.  `p2 -= 1` (Now `p2 = -1`)
    3.  `p_write -= 1` (Now `p_write = 1`)
  * **`nums1` is now:** `[ 1, 2, 2, 3, 5, 6 ]`
                        `p1, p_write`

-----

**End of Main Loop:**

  * The condition `while p1 >= 0 and p2 >= 0` is now `while 1 >= 0 and -1 >= 0`, which is `False`. The loop terminates.

-----

**Cleanup Loop:**

  * **Check:** `while p2 >= 0`
  * **Values:** `while -1 >= 0`
  * **Result:** `False`. The cleanup loop does not run.
   

---

### The Two Piles of Cards Analogy

Imagine you have two piles of sorted cards, `Pile 1` (`nums1`) and `Pile 2` (`nums2`), and you're merging them into one big pile, sorted. You're picking the **largest** card each time.

Your main rule (the main loop) is:
> "As long as I have cards in **both** `Pile 1` **AND** `Pile 2`, I will compare them and move the larger one."

`while p1 >= 0 and p2 >= 0:`

---

### The Problem (The Fail Case)

Let's say these are your piles:
* `Pile 1` (`nums1`): `[4, 5]`
* `Pile 2` (`nums2`): `[1, 2]`

You run your rule:
1.  **Compare:** `5` (from Pile 1) vs. `2` (from Pile 2).
2.  **Action:** `5` is larger. You move `5` to your new pile. `Pile 1` now only has `[4]`.
3.  **Compare:** `4` (from Pile 1) vs. `2` (from Pile 2).
4.  **Action:** `4` is larger. You move `4` to your new pile. `Pile 1` is now **empty**.

**Your main rule now stops!**
The condition `while p1 >= 0 and p2 >= 0` is **FALSE**, because `p1` is now `-1` (Pile 1 is empty).

But look! `Pile 2` (`nums2`) **still has `[1, 2]` left in it!**

---

### The Solution (The Cleanup Loop)

This is why you **must** have the second loop. The second loop is your "cleanup" rule:
> "Okay, I'm done with the main rule. Now, if `Pile 2` (`nums2`) still has any cards left in it, just move all of them over, since they are all smaller than what I've already moved."

`while p2 >= 0:`

This "cleanup" loop's only job is to handle the case where `Pile 1` (`nums1`) runs out of cards before `Pile 2` (`nums2`) does.

-----

**End of Function:**

  * The final array is `[1, 2, 2, 3, 5, 6]`. This is correct\! ✅

-----

## 🧩 7. Time & Space Analysis

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **1. Brute Force** | $O((m+n) \log(m+n))$ | $O(m+n)$ |
| **2. Three Pointers**| $O(m+n)$ | $O(1)$ |

  * **Approach 1 (Create New, Sort):** The dominant step is `merged.sort()`. Sorting an array of size $k$ takes $O(k \log k)$ time. Our array is size $m+n$, so it's $O((m+n) \log(m+n))$. We also create a new list of size $m+n$, so the space is $O(m+n)$.
  * **Approach 2 (Three Pointers):** We visit each element from `nums1` and `nums2` exactly once. This is $m + n$ operations, so the time is $O(m+n)$. We only use three pointer variables, so the space is $O(1)$.

-----

## 🧩 8. Quick Test Cases

```python
sol = Solution()

# Example 1: Standard case
nums1 = [1, 2, 3, 0, 0, 0]
sol.merge(nums1, 3, [2, 5, 6], 3)
print(nums1)  # ✅ Output: [1, 2, 2, 3, 5, 6]

# Example 2: nums2 has smaller items (tests cleanup loop)
nums1 = [4, 5, 6, 0, 0, 0]
sol.merge(nums1, 3, [1, 2, 3], 3)
print(nums1)  # ✅ Output: [1, 2, 3, 4, 5, 6]

# Example 3: nums1 is empty
nums1 = [0, 0]
sol.merge(nums1, 0, [1, 2], 2)
print(nums1)  # ✅ Output: [1, 2]

# Example 4: nums2 is empty
nums1 = [1, 2]
sol.merge(nums1, 2, [], 0)
print(nums1)  # ✅ Output: [1, 2]
```

-----

## 🧠 9. Summary Comparison

| Approach | Description | Time | Space | In-Place? |
| :--- | :--- | :--- | :--- | :--- |
| **1. Brute Force** | Create a new `merged` list, sort it, and copy it back. | $O((m+n)\log(m+n))$ | $O(m+n)$ | ❌ **No** |
| **2. Three Pointers** | Merge **backwards** from the end of `nums1`. | $O(m+n)$ | $O(1)$ | ✅ **Yes** |
