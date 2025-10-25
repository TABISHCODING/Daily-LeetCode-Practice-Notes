
-----

# 🧩 **LeetCode 15 — 3Sum**

This is a famous and essential interview problem that builds directly on the "Two Pointer" pattern. The key is turning a 3-number problem ($O(n^3)$) into a 2-number problem ($O(n^2)$).

We’ll cover:

1.  Problem Understanding
2.  Example Explanation
3.  Approach 1 — Brute Force (Three Loops + Set)
4.  Approach 2 — Sort + Two Pointers (Optimal)
5.  Full Code with Comments (Optimal)
6.  Dry Run (Step-by-Step Visual)
7.  Time & Space Analysis
8.  Quick Test Cases
9.  Summary Comparison

-----

## 🧠 1. Problem Understanding (Simplified)

We are given an array of integers, `nums`.
Our goal is to find all **unique triplets** (combinations of three numbers `[a, b, c]`) from the array that add up to **zero**.

There are two critical constraints:

1.  **Unique Triplet:** The solution `[-1, 0, 1]` is the *same* as `[0, 1, -1]`. The order of numbers inside the triplet doesn't matter.
2.  **No Duplicate Triplet:** If the input is `nums = [-1, 0, 1, -1]`, we can form `[-1, 0, 1]` using the *first* `-1` and `[-1, 0, 1]` using the *second* `-1`. Our final answer should only include `[-1, 0, 1]` **one time**.

-----

## ⚙️ 2. Example Explanation

### ⚙️ Example 1

```python
Input:  nums = [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]
```

**Explanation:**

  * `nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0`.  This gives us `[-1, 0, 1]`.
  * `nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0`. This gives us `[-1, 2, -1]`, which is the same as `[-1, -1, 2]`.
  * `nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0`. This is `[0, 1, -1]`, which is the *same* as `[-1, 0, 1]`.
  * The final *unique* set of triplets is `[[-1, -1, 2], [-1, 0, 1]]`.

-----

## 🧩 3. Approach 1 — Brute Force (Three Loops + Set)

This is the "obvious" solution that is too slow but helps understand the problem.

### 💡 **Idea**

1.  Use three nested loops (`i`, `j`, `k`) to check every possible combination of three numbers in the array.
2.  If `nums[i] + nums[j] + nums[k] == 0`, we found a potential answer.
3.  To handle the "Unique Triplet" rule, we **sort** the triplet (e.g., `[2, -1, -1]` becomes `[-1, -1, 2]`).
4.  To handle the "No Duplicate Triplet" rule, we add this sorted triplet to a **set** (which automatically stores only unique items).
5.  Finally, convert the set of triplets back into a list.

-----

### ⏱️ Time Complexity: $O(n^3)$

We have three nested loops, each running $O(n)$ times. This $O(n^3)$ is too slow and will **Time Out** on LeetCode.

### 💾 Space Complexity: $O(k)$

Where $k$ is the number of unique triplets found. The set will store $k$ triplets.

-----

### 🧾 Code — Brute Force

```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        res_set = set()
        n = len(nums)
        
        for i in range(n - 2):
            for j in range(i + 1, n - 1):
                for k in range(j + 1, n):
                    if nums[i] + nums[j] + nums[k] == 0:
                        # Sort the triplet to handle uniqueness
                        triplet = sorted([nums[i], nums[j], nums[k]])
                        # Add to set (as a tuple)
                        res_set.add(tuple(triplet))
                        
        # Convert set of tuples back to list of lists
        return [list(triplet) for triplet in res_set]
```



---

### 1. `for i in range(n - 2):`

* **`i` is the first number.**
* **Why start at `0`?** (This is the default for `range()`). We need to start at the beginning of the array.
* **Why stop at `n - 3`?** (Because `range(n-2)` goes up to, but does not include, `n-2`. So the last `i` is `n-3`).
* `i` needs to leave room for two *more* numbers, `j` and `k`, to come *after* it.
* If `i` went all the way to `n-1` (the end), there would be no room for `j` or `k`.
* If `i` went to `n-2`, `j` could be `n-1`, but there would be no room for `k`.
* So, `i` **must stop at `n-3`**, leaving `n-2` for `j` and `n-1` for `k`.

### 2. `for j in range(i + 1, n - 1):`

* **`j` is the second number.**
* **Why start at `i + 1`?** This is the most important part! By *always* starting `j` *after* `i`, we guarantee two things:
    1.  `j` is never the same index as `i`.
    2.  We don't check combinations we've already seen. (e.g., if we check `(i=0, j=1)`, we will *never* check `(i=1, j=0)`. This cuts our work in half!)
* **Why stop at `n - 2`?** (Because `range(..., n-1)` stops at `n-2`).
* This is the same logic as `i`. `j` needs to leave room for *one* more number, `k`, to come *after* it.
* The last slot `k` can take is `n-1`, so `j` must stop at `n-2`.

### 3. `for k in range(j + 1, n):`

* **`k` is the third number.**
* **Why start at `j + 1`?** Same logic as before. We force `k` to be a *different* index from `j` and `i`, and we prevent re-checking combinations.
* **Why stop at `n - 1`?** (Because `range(..., n)` stops at `n-1`).
* `k` is the last number, so it's allowed to go all the way to the end of the array.

---

### Visualization

Here's how the pointers move for an array with `n=5`: `[a, b, c, d, e]`
Indices: `0, 1, 2, 3, 4`

* **`i`** will run from `0` to `2` (`n-3`).
* **`j`** will run from `i+1` to `3` (`n-2`).
* **`k`** will run from `j+1` to `4` (`n-1`).

**When `i = 0` (at `a`):**
* `j = 1` (at `b`):
    * `k = 2` (at `c`) → `(a, b, c)`
    * `k = 3` (at `d`) → `(a, b, d)`
    * `k = 4` (at `e`) → `(a, b, e)`
* `j = 2` (at `c`):
    * `k = 3` (at `d`) → `(a, c, d)`
    * `k = 4` (at `e`) → `(a, c, e)`
* `j = 3` (at `d`):
    * `k = 4` (at `e`) → `(a, d, e)`

**When `i = 1` (at `b`):**
* `j = 2` (at `c`):
    * `k = 3` (at `d`) → `(b, c, d)`
    * `k = 4` (at `e`) → `(b, c, e)`
* `j = 3` (at `d`):
    * `k = 4` (at `e`) → `(b, d, e)`

**When `i = 2` (at `c`):**
* `j = 3` (at `d`):
    * `k = 4` (at `e`) → `(c, d, e)`

...and we're done! We've found every single unique triplet combination.
✅ Simple to understand.
❌ **Fails due to Time Limit Exceeded (TLE).**

-----

## 🧩 4. Approach 2 — Sort + Two Pointers (Optimal)

This is the standard, accepted solution. We **reduce the problem** from 3Sum to 2Sum.

### 💡 **Idea**

The key is to **sort the array first**. This $O(n \log n)$ operation lets us solve both the "duplicate" problem and the "search" problem efficiently.

The main idea: **Fix one number (`nums[i]`) and find the other two.**

`nums[i] + nums[left] + nums[right] = 0`

This is the same as:
`nums[left] + nums[right] = -nums[i]`

This is now a **Two Sum II** problem on a sorted array\! We can solve it in $O(n)$ time using the "converging" two-pointer pattern.

-----

### 🧠 Logic

1.  **Sort `nums`** ($O(n \log n)$).
2.  Loop through the array with a pointer `i`. This `nums[i]` is our "fixed" first number.
3.  **Critical: Skip Duplicates for `i`**: If `i > 0` and `nums[i]` is the *same* as `nums[i-1]`, we have already found all triplets for this number. **`continue`** to the next `i` to avoid duplicate triplets.
4.  For each `i`, set `target = -nums[i]`.
5.  Initialize two more pointers on the *rest* of the array: `left = i + 1` and `right = len(nums) - 1`.
6.  Start a `while left < right` loop (this is the Two Sum II part):
      * `current_sum = nums[left] + nums[right]`
      * **If `current_sum == target`**: We found a triplet\! `[nums[i], nums[left], nums[right]]`. Add it to our results.
          * **Critical: Skip Duplicates for `left` and `right`**: Now, we must move our pointers *past* any duplicates.
          * `while left < right and nums[left] == nums[left+1]: left += 1`
          * `while left < right and nums[right] == nums[right-1]: right -= 1`
          * After skipping, move both pointers inward: `left += 1`, `right -= 1`.
      * **If `current_sum < target`**: The sum is too small. We need a larger number, so move `left += 1`.
      * **If `current_sum > target`**: The sum is too big. We need a smaller number, so move `right -= 1`.
7.  Return the results.

-----

## 🧾 5. Full Code with Comments (Optimal)

```python
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        res = []
        # 1. Sort the array
        nums.sort()
        n = len(nums)
        
        # 2. Outer loop for the "fixed" number `nums[i]`
        for i in range(n - 2):
            
            # 3. CRITICAL: Skip duplicate 'i' values
            # If this 'i' is the same as the last 'i', we've
            # already processed all its combinations.
            if i > 0 and nums[i] == nums[i-1]:
                continue
                
            # 4. Set up the Two Sum II problem
            target = -nums[i]
            left = i + 1
            right = n - 1
            
            # 5. Inner loop (Two Pointers)
            while left < right:
                current_sum = nums[left] + nums[right]
                
                if current_sum == target:
                    # Found a triplet!
                    res.append([nums[i], nums[left], nums[right]])
                    
                    # 6. CRITICAL: Skip duplicates for 'left'
                    while left < right and nums[left] == nums[left+1]:
                        left += 1
                    
                    # 7. CRITICAL: Skip duplicates for 'right'
                    while left < right and nums[right] == nums[right-1]:
                        right -= 1
                        
                    # 8. Move pointers to find the next unique pair
                    left += 1
                    right -= 1
                    
                elif current_sum < target:
                    # Sum is too small, need a larger number
                    left += 1
                else:
                    # Sum is too large, need a smaller number
                    right -= 1
                    
        return res
```

-----

## 🧮 6. Dry Run (Step-by-Step Visual)

Here is a dry run for the "Sort + Two Pointers" algorithm.

**🎯 Input:** `nums = [-1, 0, 1, 2, -1, -4]`

**Step 1: Sort `nums`**
`nums` is now `[-4, -1, -1, 0, 1, 2]`
`n = 6`
`res = []`

-----

**`i` Loop 1: `i = 0`, `nums[i] = -4`**

  * (Skip check: `i > 0` is false).
  * `target = -(-4) = 4`
  * `left = 1` (at `-1`), `right = 5` (at `2`)
  * `while left < right`:
      * `sum = nums[left] + nums[right]` → `(-1) + 2 = 1`.
      * `1 < 4` (sum \< target). Move `left += 1`.
      * `left = 2` (at `-1`). `sum = (-1) + 2 = 1`.
      * `1 < 4` (sum \< target). Move `left += 1`.
      * `left = 3` (at `0`). `sum = 0 + 2 = 2`.
      * `2 < 4` (sum \< target). Move `left += 1`.
      * `left = 4` (at `1`). `sum = 1 + 2 = 3`.
      * `3 < 4` (sum \< target). Move `left += 1`.
      * `left = 5` (at `2`). `left < right` (5 \< 5) is **False**. Loop ends.
  * **Result:** No triplets found for `i = 0`.

-----

**`i` Loop 2: `i = 1`, `nums[i] = -1`**

  * (Skip check: `nums[1] != nums[0]`).
  * `target = -(-1) = 1`
  * `left = 2` (at `-1`), `right = 5` (at `2`)
  * `while left < right`:
      * `sum = nums[left] + nums[right]` → `(-1) + 2 = 1`.
      * `1 == 1` (sum == target). **FOUND A TRIPLET\!**
      * `res.append([-1, -1, 2])`.
      * **Skip duplicates:**
          * `while nums[left] == nums[left+1]`? `(-1) != 0`. No skip.
          * `while nums[right] == nums[right-1]`? `2 != 1`. No skip.
      * Move pointers: `left` becomes `3` (at `0`), `right` becomes `4` (at `1`).
      * `sum = nums[left] + nums[right]` → `0 + 1 = 1`.
      * `1 == 1` (sum == target). **FOUND A TRIPLET\!**
      * `res.append([-1, 0, 1])`.
      * **Skip duplicates:**
          * `while nums[left] == nums[left+1]`? `0 != 1`. No skip.
          * `while nums[right] == nums[right-1]`? `1 != 0`. No skip.
      * Move pointers: `left` becomes `4` (at `1`), `right` becomes `3` (at `0`).
      * `left < right` (4 \< 3) is **False**. Loop ends.
  * **Result:** `res = [[-1, -1, 2], [-1, 0, 1]]`

-----

**`i` Loop 3: `i = 2`, `nums[i] = -1`**

  * (Skip check: `i > 0` is true. `nums[2] == nums[1]`? `(-1) == (-1)`? **True**).
  * **Action: `continue`**. This *skips* processing and avoids a duplicate `[-1, 0, 1]`.

-----

**`i` Loop 4: `i = 3`, `nums[i] = 0`**

  * (Skip check: `0 != -1`).
  * `target = -0 = 0`
  * `left = 4` (at `1`), `right = 5` (at `2`)
  * `while left < right`:
      * `sum = 1 + 2 = 3`.
      * `3 > 0` (sum \> target). Move `right -= 1`.
      * `left = 4`, `right = 4`. `left < right` is **False**. Loop ends.
  * **Result:** No new triplets.

-----

**End of Loops:**

  * `i` loop finishes.
  * **Final Answer:** `[[-1, -1, 2], [-1, 0, 1]]`. This is correct\! ✅

-----

## 🧩 7. Time & Space Analysis

| Approach | Time Complexity | Space Complexity (Extra) |
| :--- | :--- | :--- |
| **1. Brute Force + Set** | $O(n^3)$ | $O(k)$ |
| **2. Sort + 2 Pointers**| $O(n^2)$ | $O(1)$ or $O(n)$ |

  * **Approach 1 (Brute Force):** $O(n^3)$ for loops. $O(k)$ space for the set (where $k$ is the number of unique triplets).
  * **Approach 2 (Sort + 2 Pointers):** The sort takes $O(n \log n)$. The outer `i` loop runs $O(n)$ times, and the inner `left/right` loop runs $O(n)$ time. Total time is $O(n \log n) + O(n^2)$, which simplifies to **$O(n^2)$**.
  * **Space for Approach 2:** This is debatable. The sorting algorithm (like Timsort in Python or Quicksort) can take $O(n)$ or $O(\log n)$ space. If we *only* count the extra variables `i, left, right`, it's $O(1)$. Most interviewers accept **$O(1)$** or **$O(n)$** (if you count the sort's space). We ignore the space for the *output* list.

-----

## 🧩 8. Quick Test Cases

```python
sol = Solution()

# Example 1: Standard case
print(sol.threeSum([-1, 0, 1, 2, -1, -4]))
# ✅ Output: [[-1, -1, 2], [-1, 0, 1]]

# Example 2: Empty list
print(sol.threeSum([]))
# ✅ Output: []

# Example 3: All zeros (tests duplicate skipping)
print(sol.threeSum([0, 0, 0, 0]))
# ✅ Output: [[0, 0, 0]]

# Example 4: No solution
print(sol.threeSum([1, 2, -1, -5]))
# ✅ Output: []
```

-----

## 🧠 9. Summary Comparison

| Approach | Description | Time | Space (Extra) | In-Place? |
| :--- | :--- | :--- | :--- | :--- |
| **1. Brute Force** | Three nested loops. Use a `set` to handle duplicates. | $O(n^3)$ | $O(k)$ | ❌ |
| **2. Sort + 2 Pointers**| Sort first. Fix one element (`i`), use 2-pointers (`l, r`) on the rest. | $O(n^2)$ | $O(1)$ or $O(n)$ | ✅ |
