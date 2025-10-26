
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

Here's the logic for that specific code, which doesn't use a separate `target` variable.

The core idea is:
1.  **Sort** the array. This is the most important step.
2.  **Fix one number** (`nums[i]`) with an outer loop.
3.  Use **two other pointers** (`left` and `right`) to "search" the rest of the array for two numbers that, when added to `nums[i]`, equal zero.

---

## Step-by-Step Logic

### **Preparation**
* **Step 1: `nums.sort()`**
    * **Why?** Sorting is critical. It allows us to use the two-pointer trick. If our sum is too small, we *know* we can get a bigger number by moving the `left` pointer right. If the sum is too big, we *know* we can get a smaller number by moving the `right` pointer left. It also groups all duplicates together, making them easy to skip.
* **Step 2: `res = []`**
    * Just an empty list to store our answers.

---

### **The Main Loops**
* **Step 3: `for i in range(len(nums) - 2):`**
    * This loop "fixes" our first number, `nums[i]`. We iterate through almost the whole array, leaving room (`- 2`) for the `left` and `right` pointers.
* **Step 4: `if i > 0 and nums[i] == nums[i - 1]: continue`**
    * **Logic:** This skips duplicate *answers*. For example, if `nums = [-1, -1, 0, 1]`.
    * When `i = 0` (value `-1`), we find the triplet `[-1, 0, 1]`.
    * When `i = 1` (value `-1`), this `if` statement catches it. It sees that `nums[1]` is the same as `nums[0]`. We've *already* found all triplets for the number `-1`, so we `continue` (skip) to avoid adding `[-1, 0, 1]` a second time.
* **Steps 5-7: The Two-Pointer Setup**
    * We set `left = i + 1` (just after our fixed number) and `right = len(nums) - 1` (the very end).
    * `while left < right:` just means we'll keep searching until our two pointers cross.

---

### **The Core Logic (Inside the `while` loop)**
This is where your "no target" logic comes in.

* **Step 8: `total = nums[i] + nums[left] + nums[right]`**
    * We directly calculate the sum of the three numbers we are currently pointing at.
* **Step 9-14: `if total == 0:` (We found an answer!)**
    * `Step 10`: We add the triplet to our results.
    * `Steps 11-14`: This is **crucial**. We found a valid triplet, but there might be duplicates *at the `left` and `right` pointers*.
    * `while... nums[left] == nums[left - 1]`: This skips all duplicates for the `left` pointer. For example, if we have `[...2, 2, 2, 3...]` and `nums[left]` was the first `2`, this loop moves `left` all the way to the `3` to avoid checking the same pair again.
    * `while... nums[right] == nums[right + 1]`: This does the same for the `right` pointer.
* **Step 15: `elif total < 0:` (The sum is too small)**
    * **Logic:** Our `total` is negative. We need a *larger* number to get closer to 0. Since the array is sorted, the only way to get a larger number is to move the **`left` pointer to the right** (`left += 1`).
* **Step 16: `else:` (The sum is too big, `total > 0`)**
    * **Logic:** Our `total` is positive. We need a *smaller* number. Since the array is sorted, the only way to get a smaller number is to move the **`right` pointer to the left** (`right -= 1`).

This `while` loop continues, shrinking the "window" between `left` and `right`, until they cross. Then, the main `i` loop moves to the next number, and the process repeats.
-----

---

# 🧮 Full Code (with comments)

```python
def three_sum(nums):
    nums.sort()  # Step 1
    res = []     # Step 2

    for i in range(len(nums) - 2):  # Step 3
        if i > 0 and nums[i] == nums[i - 1]:
            continue  # Step 4

        left = i + 1              # Step 5
        right = len(nums) - 1     # Step 6

        while left < right:       # Step 7
            total = nums[i] + nums[left] + nums[right]  # Step 8

            if total == 0:        # Step 9
                res.append([nums[i], nums[left], nums[right]])  # Step 10

                left += 1          # Step 11
                right -= 1         # Step 12

                # Step 13: Skip duplicates for left pointer
                while left < right and nums[left] == nums[left - 1]:
                    left += 1

                # Step 14: Skip duplicates for right pointer
                while left < right and nums[right] == nums[right + 1]:
                    right -= 1

            elif total < 0:        # Step 15
                left += 1
            else:                  # Step 16
                right -= 1

    return res                     # Step 17
```

---

# 🧠 Now Let’s Explain Every Line’s Purpose

---

### **Step 1: `nums.sort()`**

We sort the array so that:

* We can use the **two-pointer** technique (works only on sorted arrays).
* Duplicates become adjacent → easy to skip them later.

Example input:

```
nums = [-1, 0, 1, 2, -1, -4]
After sorting: [-4, -1, -1, 0, 1, 2]
```

---

### **Step 2: `res = []`**

To store all unique triplets.

---

### **Step 3: `for i in range(len(nums) - 2):`**

We fix one element `nums[i]` at a time.

We go only till `len(nums)-2` because we always need at least 2 more elements (`left`, `right`).

---

### **Step 4:**

```python
if i > 0 and nums[i] == nums[i - 1]:
    continue
```

✅ **Purpose:** Skip duplicates for the fixed element.

👉 Suppose we already used `nums[i-1] = -1`.
If the next element `nums[i]` is also `-1`,
we’ll get the *same triplets again*. So we skip it.

---

### **Step 5–6: Initialize Two Pointers**

```python
left = i + 1
right = len(nums) - 1
```

We now look for two numbers that make the sum = `-nums[i]`.

---

### **Step 7: `while left < right:`**

Loop continues while pointers haven’t crossed.

---

### **Step 8: Calculate total**

```python
total = nums[i] + nums[left] + nums[right]
```

Check whether the three numbers sum to zero.

---

### **Step 9–12: When We Find a Valid Triplet**

```python
if total == 0:
    res.append([nums[i], nums[left], nums[right]])
    left += 1
    right -= 1
```

✅ Found one valid triplet, store it.
Then we move both pointers inward to check for more combinations.

---

### **Step 13–14: Skip Duplicates Around Pointers**

This is where your question is 👇

```python
while left < right and nums[left] == nums[left - 1]:
    left += 1
```

**Why?**
If the next number on the left side is the same as the previous one,
we’ll form the same triplet again.
Example: `[-1, -1, 2]` → the next `-1` would make the same triplet again.

So we **move left forward** until we see a new value.

---

```python
while left < right and nums[right] == nums[right + 1]:
    right -= 1
```

**Why?**
Same logic for the right side.
If `nums[right]` equals the previous `nums[right+1]` (which we just used),
it’ll duplicate the same triplet.

So we **move right backward** until we see a new value.

✅ These two loops **guarantee unique triplets** in `res`.

---

### **Step 15–16: Adjust Pointers When Not Equal to 0**

```python
elif total < 0:
    left += 1
else:
    right -= 1
```

* If total < 0 → need a larger sum → move `left` (increase number)
* If total > 0 → need smaller sum → move `right` (decrease number)

---

### **Step 17: `return res`**

Finally, return all unique triplets.

---

# 🧮 DRY RUN

We’ll go through every single step exactly as the computer does — and explain *why* it takes each step.

---


## 🧩 Step-by-Step Dry Run (with 15 main steps)

---

### 🧮 STEP 1: Sort the array

```python
nums.sort()
```

Sorted:

```
nums = [-4, -1, -1, 0, 1, 2]
```

👉 Sorting helps us:

* Use two-pointer technique.
* Skip duplicates easily (since they’re next to each other).

---

### 🧮 STEP 2: Initialize result list

```python
res = []
```

Empty for now → `res = []`

---

### 🧮 STEP 3: Start loop to fix one number (`i`)

```python
for i in range(len(nums) - 2):
```

We’ll iterate `i = 0` to `3` (since last two positions are reserved for left & right pointers).

---

---

### ✅ i = 0 → nums[i] = -4

---

### 🧮 STEP 4: Skip duplicate fixed numbers

```python
if i > 0 and nums[i] == nums[i - 1]:
    continue
```

Here, `i=0`, so this check is **False** → continue normally.

---

### 🧮 STEP 5 & 6: Initialize two pointers

```python
left = i + 1 = 1
right = len(nums) - 1 = 5
```

Pointers:

```
i=0 (-4), left=1 (-1), right=5 (2)
```

---

### 🧮 STEP 7: While loop condition

`while left < right:` → (1 < 5) ✅

---

### 🧮 STEP 8: Calculate total

```python
total = nums[i] + nums[left] + nums[right]
       = (-4) + (-1) + (2) = -3
```

---

### 🧮 STEP 9–16: Compare `total`

* `total < 0` → move `left` pointer right

```python
left += 1
```

Now `left = 2` (nums[left] = -1)

---

### 🧮 STEP 8 again

```
total = (-4) + (-1) + (2) = -3
```

Still `< 0` → move left again → `left = 3 (0)`

---

Next:

```
total = (-4) + (0) + (2) = -2 < 0
→ left = 4 (1)
```

Next:

```
total = (-4) + (1) + (2) = -1 < 0
→ left = 5
```

Now `left = right` → while loop ends.

No triplet found for i=0.

---

---

### ✅ i = 1 → nums[i] = -1

---

### 🧮 STEP 4: Duplicate check

```
i > 0 → True
nums[i] == nums[i-1]? → (-1 == -4)? No
```

So continue.

---

### 🧮 STEP 5–6: Initialize pointers

```
left = 2, right = 5
```

→ left=2 (-1), right=5 (2)

---

### 🧮 STEP 7: while (2 < 5) → ✅

---

### 🧮 STEP 8: total

```
total = (-1) + (-1) + (2) = 0
```

---

### 🧮 STEP 9: Found triplet 🎯

```
res.append([-1, -1, 2])
res = [[-1, -1, 2]]
```

---

### 🧮 STEP 11–12: Move both pointers inward

```
left = 3, right = 4
```

---

### 🧮 STEP 13: Skip duplicates for left

```
while left < right and nums[left] == nums[left - 1]
→ nums[3]=0, nums[2]=-1 → not equal → skip
```

No duplicate on left.

---

### 🧮 STEP 14: Skip duplicates for right

```
nums[4]=1, nums[5]=2 → not equal → skip
```

No duplicate on right.

---

### 🧮 STEP 7 again: (3 < 4) ✅

---

### 🧮 STEP 8: total

```
total = (-1) + (0) + (1) = 0 ✅
```

---

### 🧮 STEP 9: Found triplet 🎯

```
res.append([-1, 0, 1])
res = [[-1, -1, 2], [-1, 0, 1]]
```

---

### 🧮 STEP 11–12: Move both pointers

```
left = 4, right = 3
```

Now `left > right` → while loop ends.

---

### ✅ STEP 3 → next i

---

### ✅ i = 2 → nums[i] = -1

---

### 🧮 STEP 4: Duplicate check

```
nums[i] == nums[i-1]? (-1 == -1)? ✅ True
→ continue
```

Skip this i (because we already processed -1 before).

---

### ✅ i = 3 → nums[i] = 0

---

### 🧮 STEP 4: Duplicate check

```
nums[3]=0, nums[2]=-1 → not equal → continue
```

---

### 🧮 STEP 5–6: Initialize pointers

```
left = 4, right = 5
```

---

### 🧮 STEP 7: while (4 < 5) ✅

---

### 🧮 STEP 8: total

```
total = (0) + (1) + (2) = 3 > 0
```

---

### 🧮 STEP 16: Move right pointer left

```
right = 4
```

Now `left == right` → stop.

---

### ✅ Loop ends (i goes beyond limit)

---

### 🧮 STEP 17: Return result

```
res = [[-1, -1, 2], [-1, 0, 1]]
```

🎉 **Final Output:**

```python
[[-1, -1, 2], [-1, 0, 1]]
```

---

## 🧾 Summary Table of Each Major Step

| Step  | What Happens                          | Why                                            |
| ----- | ------------------------------------- | ---------------------------------------------- |
| 1     | Sort array                            | Needed for 2-pointer logic                     |
| 2     | Initialize result list                | To store valid triplets                        |
| 3     | Loop through each number as fixed `i` | To pick one number for 3Sum                    |
| 4     | Skip duplicate `i`                    | Avoid repeating same triplets                  |
| 5–6   | Set left/right pointers               | To search for 2 numbers that balance `nums[i]` |
| 7     | While loop                            | Scan the range for valid pairs                 |
| 8     | Compute `total`                       | Sum of 3 numbers                               |
| 9–10  | If total==0                           | Found triplet, store it                        |
| 11–12 | Move pointers                         | Continue searching for next possible pairs     |
| 13    | Skip left duplicates                  | Prevent same triplet again                     |
| 14    | Skip right duplicates                 | Same reason as above                           |
| 15    | If total < 0                          | Need bigger numbers → move left                |
| 16    | If total > 0                          | Need smaller numbers → move right              |
| 17    | Return all unique triplets            | Done ✅                                         |

---




# 🔁 What Happens If We REMOVE Duplicate-Skipping Lines?

Try removing:

```python
if i > 0 and nums[i] == nums[i - 1]: continue
```

Then for i=1 and i=2 (both = -1), you’ll get the **same triplets twice**.

Try removing:

```python
while left < right and nums[left] == nums[left - 1]: left += 1
while left < right and nums[right] == nums[right + 1]: right -= 1
```

Then inside the same loop, if you have repeated numbers like `[-1, -1, 2]`,
you’ll store duplicates like `[[-1, -1, 2], [-1, -1, 2]]`.

So these lines make your answer **clean and unique** ✅

---




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




---

