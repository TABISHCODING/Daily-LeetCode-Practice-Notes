
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
**DRY RUN with explanation**
---



Think of it like picking a team of 3 people from a line of 6: `[A, B, C, D, E, F]`

If you just use three separate loops (`for i in range(6)`, `for j in range(6)`, `for k in range(6)`), you would check terrible combinations:
* `[A, A, A]` (pointers are the same)
* `[A, B, C]` (this is a good one!)
* `[C, B, A]` (this is the *same team*! We don't want to check it again).

---

### The "No Going Backward" Rule
To solve this, we invent a simple rule: **"To make a team, I will only pick people from left-to-right. I will never go backward."**

This is what your nested loops do!

#### 1. The `i` loop (First Team Member)
`for i in range(n - 2):`

This loop picks the *first* person.
* Let's say `i` picks **`A`** (index 0).

#### 2. The `j` loop (Second Team Member)
`for j in range(i + 1, n - 1):`

* **`range(i + 1, ...)`** is the "No Going Backward" rule!
* It forces `j` to start *after* `i`.
* `j` *must* start by picking **`B`** (index 1). It is not allowed to pick `A` again.

#### 3. The `k` loop (Third Team Member)
`for k in range(j + 1, n):`

* **`range(j + 1, ...)`** is the same rule again!
* It forces `k` to start *after* `j`.
* `k` *must* start by picking **`C`** (index 2).

This system guarantees that `i`, `j`, and `k` are **always different** and that you **never check the same combination twice.**

---

### Why `n-2`, `n-1`, `n`? (The "Last Team" Rule)
This just makes sure your loops don't crash when you run out of people.

Let's find the **last possible team** in the line: `[A, B, C, D, E, F]`

The last team you can possibly pick is **`[D, E, F]`**.
* **`i`** is at `D` (index `3`)
* **`j`** is at `E` (index `4`)
* **`k`** is at `F` (index `5`)

This tells us the *last* index each pointer ever needs to touch:
* The **`i`** loop (first person) only needs to go up to **`D`** (index `3`). If `i` picked `E`, there wouldn't be two people left for `j` and `k`!
* The **`j`** loop (second person) only needs to go up to **`E`** (index `4`).
* The **`k`** loop (third person) needs to go all the way to **`F`** (index `5`).

Now look at the code when `n = 6`:
* `range(n - 2)` $\rightarrow$ `range(4)` $\rightarrow$ `0, 1, 2, 3`. **Last index is `3` (`D`)**. ✅
* `range(..., n - 1)` $\rightarrow$ `range(..., 5)` $\rightarrow$ `...3, 4`. **Last index is `4` (`E`)**. ✅
* `range(..., n)` $\rightarrow$ `range(..., 6)` $\rightarrow$ `...4, 5`. **Last index is `5` (`F`)**. ✅

The ranges are set up to stop *exactly* at the last possible spot each pointer can be.

---

### How the `if` Check Fits In (Full Example)

The `if nums[i] + nums[j] + nums[k] == 0:` check happens **inside the innermost `k` loop**. It is the *last* thing that happens, right after you've picked your team of three.

Let's use `nums = [-1, 0, 1, 2, -1, -4]` (`n=6`).

#### `i` is set to 0. (value `nums[0] = -1`)
* `j` is set to 1. (value `nums[1] = 0`)
    * `k` is set to 2. (value `nums[2] = 1`)
        * **CHECK:** `if (-1) + 0 + 1 == 0`? **True.** Found a triplet!
    * `k` is set to 3. (value `nums[3] = 2`)
        * **CHECK:** `if (-1) + 0 + 2 == 0`? **False.** (Sum is 1)
    * `k` is set to 4. (value `nums[4] = -1`)
        * **CHECK:** `if (-1) + 0 + (-1) == 0`? **False.** (Sum is -2)
    * `k` is set to 5. (value `nums[5] = -4`)
        * **CHECK:** `if (-1) + 0 + (-4) == 0`? **False.** (Sum is -5)
    * *(`k` loop finishes)*
* `j` is set to 2. (value `nums[2] = 1`)
    * `k` is set to 3. (value `nums[3] = 2`)
        * **CHECK:** `if (-1) + 1 + 2 == 0`? **False.** (Sum is 2)
    * `k` is set to 4. (value `nums[4] = -1`)
        * **CHECK:** `if (-1) + 1 + (-1) == 0`? **False.** (Sum is -1)
    * `k` is set to 5. (value `nums[5] = -4`)
        * **CHECK:** `if (-1) + 1 + (-4) == 0`? **False.** (Sum is -4)
    * *(`k` loop finishes)*
* `j` is set to 3. (value `nums[3] = 2`)
    * `k` is set to 4. (value `nums[4] = -1`)
        * **CHECK:** `if (-1) + 2 + (-1) == 0`? **True.** Found a triplet!
    * `k` is set to 5. (value `nums[5] = -4`)
        * **CHECK:** `if (-1) + 2 + (-4) == 0`? **False.** (Sum is -3)
    * *(`k` loop finishes)*
* `j` is set to 4. (value `nums[4] = -1`)
    * `k` is set to 5. (value `nums[5] = -4`)
        * **CHECK:** `if (-1) + (-1) + (-4) == 0`? **False.** (Sum is -6)
    * *(`k` loop finishes)*
* *(`j` loop finishes)*

#### `i` is set to 1. (value `nums[1] = 0`)
* `j` is set to 2. (value `nums[2] = 1`)
    * `k` is set to 3. (value `nums[3] = 2`)
        * **CHECK:** `if 0 + 1 + 2 == 0`? **False.**
    * ... (and so on) ...

This "odometer" process continues, checking every single team *exactly once*.

---

### When The Loops Finish
The loops run until the **very last team** `[D, E, F]` (or indices `[3, 4, 5]`) is checked.

* **Final `i` loop:** `i = 3` (value `nums[3] = 2`)
    * **Final `j` loop:** `j = 4` (value `nums[4] = -1`)
        * **Final `k` loop:** `k = 5` (value `nums[5] = -4`)
            * **FINAL CHECK:** `if 2 + (-1) + (-4) == 0`? **False.** (Sum is -3)
        * *(`k` loop finishes)*
    * *(`j` loop finishes)*
* *(`i` loop finishes)*

**Now, all loops are finished.** The `i` loop tries to go to `4`, but `range(4)` is done. The function has checked every possible unique combination and can now return the set of triplets it found.
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
