
-----

# 🧩 **LeetCode 283 — Move Zeroes**

This is a classic array manipulation problem, perfectly solved using the **Two Pointer** technique you've been practicing.

We’ll cover:

1.  Problem Understanding
2.  Example Explanation
3.  Approach 1 — Brute Force (Using Extra Space)
4.  Approach 2 — Two Pointer (Optimal, In-Place)
5.  Full Code with Comments
6.  Dry Run (Step-by-Step Visual)
7.  Quick Test Cases
8.  Summary Comparison

-----

## 🧠 1. Problem Understanding (Simplified)

We are given an array of integers, `nums`.
We must modify the array **in-place** to move all `0`'s to the **end** of the array.

There are two critical rules:

1.  All the **non-zero** elements must stay in their **original relative order**.
2.  We must do this **in-place** (without making a copy of the array).

We don't need to return anything; we just modify the `nums` list directly.

-----

## ⚙️ 2. Example Explanation

### ⚙️ Example 1

```python
Input:  nums = [0, 1, 0, 3, 12]
Output: nums = [1, 3, 12, 0, 0]
```

**Explanation:**

  * The non-zero elements are `1`, `3`, and `12`.
  * Notice their order (`1`...`3`...`12`) is preserved.
  * The two `0`'s are moved to the end.

### ⚙️ Example 2

```python
Input:  nums = [0]
Output: nums = [0]
```

**Explanation:**
The array is already in the correct state.

-----

## 🧩 3. Approach 1 — Brute Force (Using Extra Space)

This approach is simple to understand but **violates the "in-place" constraint**.

### 💡 **Idea**

1.  Create a new, empty list (e.g., `non_zeroes`).
2.  Iterate through the original `nums` array. If an element is **not** zero, append it to `non_zeroes`.
3.  Count how many zeros we saw (or calculate `num_zeroes = len(nums) - len(non_zeroes)`).
4.  Append that many `0`'s to the end of the `non_zeroes` list.
5.  Finally, copy all elements from `non_zeroes` back into the original `nums` array.

-----

### ⏱️ Time Complexity: $O(n)$

We iterate through `nums` once ($O(n)$) and then copy the data back ($O(n)$). This is $O(n) + O(n) = O(n)$.

### 💾 Space Complexity: $O(n)$

We create a new list `non_zeroes` which, in the worst case (no zeros), will be the same size as `nums`.

-----

### 🧾 Code — Brute Force

```python
class Solution:
    def moveZeroes(self, nums: list[int]) -> None:
        """
        Do not return anything, modify nums in-place.
        (This solution is NOT in-place, but shows the logic)
        """
        # 1. Create a new list for non-zero elements
        non_zeroes = []
        
        # 2. Add all non-zero elements
        for num in nums:
            if num != 0:
                non_zeroes.append(num)
        
        # 3. Calculate how many zeros we need
        num_zeroes = len(nums) - len(non_zeroes)
        
        # 4. Add the zeros to the end
        for _ in range(num_zeroes):
            non_zeroes.append(0)
            
        # 5. Copy everything back into nums
        for i in range(len(nums)):
            nums[i] = non_zeroes[i]
```

✅ Simple logic.
❌ **Fails the $O(1)$ space (in-place) constraint.**

-----

## 🧩 4. Approach 2 — Two Pointer (Optimal, In-Place)

This is the **Variation 2 (Same Direction)** pattern from your notes. We use a "Gatekeeper" and an "Explorer" to modify the array in-place.

### 💡 **Idea**

We use **two pointers**, `slow` and `fast`, both starting at index `0`.

| Pointer | Meaning (Job) |
| :--- | :--- |
| `slow` | **The Gatekeeper** 📝<br>Points to the next **empty slot** where a non-zero number should be placed. |
| `fast` | **The Explorer** 🕵️<br>Scans the entire array from beginning to end to *find* the next non-zero number. |

-----

### 🧠 Logic (The "Swap" Method)

1.  Initialize `slow = 0`.
2.  Start the `fast` pointer in a loop from `0` to the end of the array.
3.  At each element `nums[fast]`:
      * **If `nums[fast]` is NOT a zero:**
          * This is an item we need to keep\! We **swap** its position with the "Gatekeeper's" position: `nums[slow], nums[fast] = nums[fast], nums[slow]`.
          * Now that the `slow` position is filled with a non-zero number, we move the gatekeeper one step forward: `slow += 1`.
      * **If `nums[fast]` IS a zero:**
          * The explorer (`fast`) just moves on. We do nothing. The `slow` pointer stays where it is, waiting to be filled.

This process naturally "bubbles" all non-zero elements to the front (in order\!) and leaves the zeros behind.

-----

### ⏱️ **Time Complexity:** $O(n)$

The `fast` pointer iterates through the entire array exactly once.

### 💾 **Space Complexity:** $O(1)$

We only use two pointer variables (`slow`, `fast`). All modifications are done **in-place**.

-----

## 🧾 5. Full Code with Comments

```python
class Solution:
    def moveZeroes(self, nums: list[int]) -> None:
        """
        Do not return anything, modify nums in-place.
        Uses the optimal Two Pointer (Swap) method.
        """
        
        # slow is the "Gatekeeper"
        # It points to the next slot to be filled by a non-zero number.
        slow = 0
        
        # fast is the "Explorer"
        # It scans the entire array.
        for fast in range(len(nums)):
            
            # 1. Explorer (fast) finds a non-zero number
            if nums[fast] != 0:
                
                # 2. Swap the non-zero item with the gatekeeper's slot
                # (If slow == fast, this swaps an item with itself,
                # which is harmless)
                nums[slow], nums[fast] = nums[fast], nums[slow]
                
                # 3. Move the gatekeeper forward to the next empty slot
                slow += 1
```

-----

## 🧮 6. Dry Run (Step-by-Step Visual)

Here is a dry run for the "Move Zeroes" algorithm, just like we did for "Remove Duplicates."

### The Pointers' Jobs

Think of the two pointers, `slow` and `fast`, as having different jobs:

  * **`slow` (The Gatekeeper) 📝**

      * `slow`'s job is to point to the **next available slot where a non-zero number should go**.
      * It only moves forward *after* it has placed a non-zero number.

  * **`fast` (The Explorer) 🕵️**

      * `fast`'s job is to move forward one step at a time and **explore every element**.
      * Its mission is to find the next *non-zero* number.

The logic is: "The Explorer (`fast`) scans the array. When it finds a non-zero number, it **swaps** that number with whatever is at the Gatekeeper's (`slow`) position. Then, the Gatekeeper moves one step forward."

### Dry Run Example

Let's use `nums = [0, 1, 0, 3]`

**Initial State:**
`slow = 0`
The `fast` loop will start at `fast = 0`.
`nums = [ 0, 1, 0, 3 ]`
               `s` (slow)
               `f` (fast)

-----

**Loop 1: `fast = 0`**

  * **Pointers:** `slow = 0`, `fast = 0`
  * **`nums`:** `[ 0, 1, 0, 3 ]`
                        `s,f`
  * **Check:** `if nums[fast] != 0`
  * **Values:** `if 0 != 0`
  * **Result:** `False` (It's a zero).
  * **Action:** Nothing happens. `slow` does not move.

-----

**Loop 2: `fast = 1`**

  * **Pointers:** `slow = 0`, `fast = 1`
  * **`nums`:** `[ 0, 1, 0, 3 ]`
                        `s`   `f`
  * **Check:** `if nums[fast] != 0`
  * **Values:** `if 1 != 0`
  * **Result:** `True` (We found a non-zero number\!)
  * **Action:**
    1.  **Swap:** `nums[slow], nums[fast] = nums[fast], nums[slow]`
          * `nums[0], nums[1] = nums[1], nums[0]`
          * `nums[0], nums[1] = 1, 0`
    2.  **`nums` array is now:** `[ 1, 0, 0, 3 ]`
    3.  **Increment `slow`:** `slow += 1` (Now `slow = 1`). The gatekeeper moves to the next empty slot.
  * **Pointers at end of loop:** `slow = 1`, `fast = 1`
                            `s,f`

-----

**Loop 3: `fast = 2`**

  * **Pointers:** `slow = 1`, `fast = 2`
  * **`nums`:** `[ 1, 0, 0, 3 ]`
                            `s`   `f`
  * **Check:** `if nums[fast] != 0`
  * **Values:** `if 0 != 0`
  * **Result:** `False` (It's a zero).
  * **Action:** Nothing happens. `slow` does not move.

-----

**Loop 4: `fast = 3`**

  * **Pointers:** `slow = 1`, `fast = 3`
  * **`nums`:** `[ 1, 0, 0, 3 ]`
                            `s`       `f`
  * **Check:** `if nums[fast] != 0`
  * **Values:** `if 3 != 0`
  * **Result:** `True` (We found another non-zero number\!)
  * **Action:**
    1.  **Swap:** `nums[slow], nums[fast] = nums[fast], nums[slow]`
          * `nums[1], nums[3] = nums[3], nums[1]`
          * `nums[1], nums[3] = 3, 0`
    2.  **`nums` array is now:** `[ 1, 3, 0, 0 ]`
    3.  **Increment `slow`:** `slow += 1` (Now `slow = 2`). The gatekeeper moves to the next empty slot.
  * **Pointers at end of loop:** `slow = 2`, `fast = 3`
                               `s`   `f`

-----

**End of Loop**

  * `fast` has reached the end of the array. The loop stops.
  * The final array is `[ 1, 3, 0, 0 ]`.
  * All non-zero elements (`1`, `3`) are at the front.
  * All zeroes are at the end. This is correct\! ✅

-----

## 🧩 7. Quick Test Cases

```python
sol = Solution()

nums1 = [0, 1, 0, 3, 12]
sol.moveZeroes(nums1)
print(nums1)  # ✅ Output: [1, 3, 12, 0, 0]

nums2 = [0]
sol.moveZeroes(nums2)
print(nums2)  # ✅ Output: [0]

nums3 = [1, 2, 3]
sol.moveZeroes(nums3)
print(nums3)  # ✅ Output: [1, 2, 3]

nums4 = [0, 0]
sol.moveZeroes(nums4)
print(nums4)  # ✅ Output: [0, 0]
```

-----

## 🧠 8. Summary Comparison

| Approach | Description | Time | Space | In-Place? |
| :--- | :--- | :--- | :--- | :--- |
| **1. Brute Force** | Use a new list to store non-zeros, then copy back. | $O(n)$ | $O(n)$ | ❌ **No** |
| **2. Two Pointer** | Use `slow` and `fast` pointers to swap elements. | $O(n)$ | $O(1)$ | ✅ **Yes** |
