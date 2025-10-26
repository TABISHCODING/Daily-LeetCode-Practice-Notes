
-----

# 🧩 **LeetCode 11 — Container with Most Water**

This is a classic "Two Pointer" problem. It seems like it requires checking every pair, but there's a clever trick to solve it in linear time.

We’ll cover:

1.  Problem Understanding
2.  Example Explanation
3.  Approach 1 — Brute Force (Two Loops)
4.  Approach 2 — Two Pointers (Optimal, In-Place)
5.  Full Code with Comments (Optimal)
6.  Dry Run (Step-by-Step Table)
7.  Time & Space Analysis
8.  Quick Test Cases
9.  Summary Comparison

-----

## 🧠 1. Problem Understanding (Simplified)

We are given an array of non-negative integers called `height`. Each number `height[i]` represents the height of a vertical line at position `i`.

Our goal is to find **two** lines in this array that, when combined with the x-axis, form a container that can hold the **most water**.

**The formula for the area is:**
`Area = width * height`

  * **Width:** The distance between the two lines (`j - i`).
  * **Height:** The height of the *shorter* of the two lines (since water will spill over the shorter side). `min(height[i], height[j])`.

We just need to return the *maximum possible area* (a single integer).

-----

## ⚙️ 2. Example Explanation

### ⚙️ Example 1

```python
Input:  height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
Output: 49
```

**Explanation:**

We need to find the pair of lines that gives the biggest area.

  * If we pick the two `8`'s (at index 1 and 6):
      * `width = 6 - 1 = 5`
      * `height = min(8, 8) = 8`
      * `Area = 5 * 8 = 40`
  * If we pick the `8` (at index 1) and the `7` (at index 8):
      * `width = 8 - 1 = 7`
      * `height = min(8, 7) = 7`
      * `Area = 7 * 7 = 49`

After checking all pairs, `49` is the largest area we can get.

-----

## 🧩 3. Approach 1 — Brute Force (Two Loops)

This is the "obvious" solution where we literally check every single possible pair of lines.

### 💡 **Idea**

1.  Initialize a variable `max_area = 0`.
2.  Use an outer loop `i` to pick the **left line**.
3.  Use an inner loop `j` (starting from `i + 1`) to pick the **right line**.
4.  For *every pair* (`i`, `j`), calculate their area:
      * `width = j - i`
      * `h = min(height[i], height[j])`
      * `area = h * width`
5.  If this new `area` is bigger than `max_area`, update `max_area`.
6.  After all loops finish, return `max_area`.

-----

### ⏱️ Time Complexity: $O(n^2)$

We have two nested loops. The outer loop runs $n$ times, and the inner loop runs roughly $n/2$ times on average. This is $O(n^2)$.

### 💾 Space Complexity: $O(1)$

We only use a few extra variables (`max_area`, `width`, `h`, `area`).

-----

### 🧾 Code — Brute Force

```python
class Solution:
    def maxArea(self, height: list[int]) -> int:
        max_area = 0
        n = len(height)
        
        # i is the left line
        for i in range(n - 1):
            # j is the right line
            for j in range(i + 1, n):
                # Calculate the area for this pair
                width = j - i
                h = min(height[i], height[j])
                area = h * width
                
                # Update the max if this area is bigger
                max_area = max(max_area, area)
                
        return max_area
```

✅ Simple logic.
❌ **Fails due to Time Limit Exceeded (TLE)** on large inputs.

-----

## 🧩 4. Approach 2 — Two Pointers (Optimal, In-Place)

This is the clever $O(n)$ solution. It's a classic example of the "converging" or "shrinking window" two-pointer pattern.

### 💡 **Idea**

Instead of starting with the smallest width and checking all pairs, let's start with the **widest possible container** and "shrink" it.

1.  Start one pointer `left` at the beginning (`0`) and one pointer `right` at the very end (`len(height) - 1`).
2.  Calculate the area for this container. This is our `max_area` for now.
3.  Now, we need to move one of the pointers inward to find a new container. Which one?
4.  **The Key Logic:** The area is *always* limited by the **shorter line**.
      * Let's say `height[left]` is `3` and `height[right]` is `8`. Our current height is `3`.
      * If we move the `right` pointer inward, our `width` will *decrease*, and our new height will be `min(3, height[right-1])`. The height can *never* be more than `3`. So, the new area will **definitely be smaller**. This is a useless move.
      * If we move the `left` pointer inward, our `width` *also* decreases, but our new height will be `min(height[left+1], 8)`. Our height *might* be taller than `3`. This is the **only move that has a chance** of finding a larger area.

### 🧠 Logic

1.  Initialize `max_area = 0`.
2.  Initialize `left = 0` and `right = len(height) - 1`.
3.  Loop `while left < right`:
      * Calculate `width = right - left`.
      * Calculate `h = min(height[left], height[right])`.
      * Update `max_area = max(max_area, h * width)`.
      * **If `height[left] < height[right]`**: The left line is the shorter one. Moving it (`left += 1`) is the only way to *potentially* find a larger area.
      * **Else (`height[left] >= height[right]`)**: The right line is shorter (or they're equal). Moving it (`right -= 1`) is the only way to *potentially* find a larger area.
4.  When the loop finishes (`left` meets `right`), return `max_area`.

-----

## 🧾 5. Full Code with Comments (Optimal)

```python
class Solution:
    def maxArea(self, height: list[int]) -> int:
        
        max_area = 0
        left = 0
        right = len(height) - 1
        
        # Loop as long as the two pointers haven't crossed
        while left < right:
            
            # 1. Calculate the area for the current container
            width = right - left
            h = min(height[left], height[right])
            area = h * width
            
            # 2. Update the max area found so far
            max_area = max(max_area, area)
            
            # 3. The key step: move the pointer of the shorter line
            # This is because moving the taller line can only
            # decrease the width, and the height is already
            # limited by the shorter line. We need to find a
            # potentially taller line to offset the loss of width.
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
                
        return max_area
```

-----

## 🧮 6. Dry Run (Step-by-Step Table)


### The Core Logic (The Rule)

At every step, we will:

1.  Calculate the area of the current container.
2.  Check: Which line is **shorter**?
3.  Move the pointer of the **shorter** line inward.
The rule is: Always move the pointer of the shorter line. Why? Because the area is width * min_height. Moving the taller line will always decrease the width and can never increase the min_height (it's already limited by the short side). Moving the shorter line is the only move that has a chance of finding a taller line, which might create a larger area, even with a smaller width.
4.  If they are equal, we'll just move the `right` pointer (as our code does).

---
**visualize with example  to explain that logic of point 3.**
---
Let's imagine this is our `height` array. We'll start with our pointers at both ends.

**Initial State:**
`L=0`, `R=4`
`height = [ 3, 8, 4, 9, 5 ]`

Here's a diagram:

```
      8     9
      |     |     5
      |  4  |     |
 3    |  |  |     |
 |    |  |  |     |
 |    |  |  |     |
---L----|--|--|----R---  (Index 0 to 4)
```

  * **Left Line (`L`):** `height[0] = 3`
  * **Right Line (`R`):** `height[4] = 5`
  * **Width:** `4 - 0 = 4`
  * **Height:** `min(3, 5) = 3` (The water is limited by the **shorter line**, `L`)
  * **Current Area:** `4 * 3 = 12`

Now, we have to move one pointer.

-----

### Choice 1: The *Wrong* Move (Move the Taller Pointer `R`)

Let's see what happens if we ignore the rule and move the **taller line (`R`)** inward.
`L=0`, `R=3`

```
      8     9
      |     |
      |  4  |
 3    |  |  |
 |    |  |  |
 |    |  |  |
---L----|--|--R---       (Index 0 to 3)
```

  * **Left Line (`L`):** `height[0] = 3`
  * **Right Line (`R`):** `height[3] = 9`
  * **New Width:** `3 - 0 = 3` (Width **decreased** 🔻)
  * **New Height:** `min(3, 9) = 3` (Height **stayed the same** 😐)
  * **New Area:** `3 * 3 = 9` (Area is **smaller** 🔻)

**Why this failed:** Our height was *already* limited to `3` by the `L` pointer. Moving the taller `R` pointer didn't change this. We just lost `width` for no gain. This move is **guaranteed** to result in a smaller or equal area.

-----

### Choice 2: The *Correct* Move (Move the Shorter Pointer `L`)

Now, let's follow the rule and move the **shorter line (`L`)** inward.
`L=1`, `R=4`

```
      8     9
      |     |     5
      |  4  |     |
      |  |  |     |
      |  |  |     |
      |  |  |     |
------L--|--|----R---    (Index 1 to 4)
```

  * **Left Line (`L`):** `height[1] = 8`
  * **Right Line (`R`):** `height[4] = 5`
  * **New Width:** `4 - 1 = 3` (Width **decreased** 🔻)
  * **New Height:** `min(8, 5) = 5` (Height **INCREASED\!** ⬆️)
  * **New Area:** `3 * 5 = 15` (Area is **BIGGER\!** ⬆️)

**Why this worked:** By moving the shorter line (`L`), we gave ourselves the **chance** to find a new, taller line. In this case, we found `8`, which was taller than `R`'s height of `5`, so our new limiting height became `5`.

We traded a little `width` for a lot of `height`, and it paid off. This is the **only** move that gives you the *potential* to find a larger area.

-----

### The Full Dry Run

**🎯 Input:** `height = [1, 8, 6, 2, 5, 4, 8, 3, 7]`
**⚙️ Setup:** `max_area = 0`, `left = 0`, `right = 8`

-----

### Loop 1

**State:**

```
  L                           R
  [ 1, 8, 6, 2, 5, 4, 8, 3, 7 ]
```

  * **Values:** `height[L] = 1`, `height[R] = 7`
  * **Calculate:** `width = 8`, `min_h = min(1, 7) = 1`. `Area = 8 * 1 = 8`.
  * **Update Max:** `max_area` is now `8`.
  * **Logic:** `if 1 < 7:` is **True**.
  * **Action:** The Left line is shorter. We must move it. ➡️ `left += 1`.

-----

### Loop 2

**State:**

```
    L                         R
  [ 1, 8, 6, 2, 5, 4, 8, 3, 7 ]
```

  * **Values:** `height[L] = 8`, `height[R] = 7`
  * **Calculate:** `width = 7`, `min_h = min(8, 7) = 7`. `Area = 7 * 7 = 49`.
  * **Update Max:** `max_area` is now `49`.
  * **Logic:** `if 8 < 7:` is **False**.
  * **Action:** The Right line is shorter. We must move it. ⬅️ `right -= 1`.

-----

### Loop 3

**State:**

```
    L                       R
  [ 1, 8, 6, 2, 5, 4, 8, 3, 7 ]
```

  * **Values:** `height[L] = 8`, `height[R] = 3`
  * **Calculate:** `width = 6`, `min_h = min(8, 3) = 3`. `Area = 6 * 3 = 18`.
  * **Update Max:** `max_area` is still `49`.
  * **Logic:** `if 8 < 3:` is **False**.
  * **Action:** The Right line is shorter. We must move it. ⬅️ `right -= 1`.

-----

### Loop 4

**State:**

```
    L                     R
  [ 1, 8, 6, 2, 5, 4, 8, 3, 7 ]
```

  * **Values:** `height[L] = 8`, `height[R] = 8`
  * **Calculate:** `width = 5`, `min_h = min(8, 8) = 8`. `Area = 5 * 8 = 40`.
  * **Update Max:** `max_area` is still `49`.
  * **Logic:** `if 8 < 8:` is **False**. (They are equal).
  * **Action:** The `else` block runs. We move the Right line. ⬅️ `right -= 1`.

-----

### Loop 5

**State:**

```
    L                   R
  [ 1, 8, 6, 2, 5, 4, 8, 3, 7 ]
```

  * **Values:** `height[L] = 8`, `height[R] = 4`
  * **Calculate:** `width = 4`, `min_h = min(8, 4) = 4`. `Area = 4 * 4 = 16`.
  * **Update Max:** `max_area` is still `49`.
  * **Logic:** `if 8 < 4:` is **False**.
  * **Action:** The Right line is shorter. We must move it. ⬅️ `right -= 1`.

-----

### Loop 6

**State:**

```
    L                 R
  [ 1, 8, 6, 2, 5, 4, 8, 3, 7 ]
```

  * **Values:** `height[L] = 8`, `height[R] = 5`
  * **Calculate:** `width = 3`, `min_h = min(8, 5) = 5`. `Area = 3 * 5 = 15`.
  * **Update Max:** `max_area` is still `49`.
  * **Logic:** `if 8 < 5:` is **False**.
  * **Action:** The Right line is shorter. We must move it. ⬅️ `right -= 1`.

-----

### Loop 7

**State:**

```
    L               R
  [ 1, 8, 6, 2, 5, 4, 8, 3, 7 ]
```

  * **Values:** `height[L] = 8`, `height[R] = 2`
  * **Calculate:** `width = 2`, `min_h = min(8, 2) = 2`. `Area = 2 * 2 = 4`.
  * **Update Max:** `max_area` is still `49`.
  * **Logic:** `if 8 < 2:` is **False**.
  * **Action:** The Right line is shorter. We must move it. ⬅️ `right -= 1`.

-----

### Loop 8

**State:**

```
    L             R
  [ 1, 8, 6, 2, 5, 4, 8, 3, 7 ]
```

  * **Values:** `height[L] = 8`, `height[R] = 6`
  * **Calculate:** `width = 1`, `min_h = min(8, 6) = 6`. `Area = 1 * 6 = 6`.
  * **Update Max:** `max_area` is still `49`.
  * **Logic:** `if 8 < 6:` is **False**.
  * **Action:** The Right line is shorter. We must move it. ⬅️ `right -= 1`.

-----

### End of Program

**State:**

```
    L,R
  [ 1, 8, 6, 2, 5, 4, 8, 3, 7 ]
```

  * The `while` loop checks its condition: `while left < right:`
  * The values are `while 1 < 1:`.
  * This is **FALSE**. The loop terminates.
  * The function `return max_area`.
  * **Final Answer:** `49`.
-----

## 🧩 7. Time & Space Analysis

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **1. Brute Force** | $O(n^2)$ | $O(1)$ |
| **2. Two Pointers**| $O(n)$ | $O(1)$ |

  * **Approach 1 (Brute Force):** Two nested loops make it $O(n^2)$.
  * **Approach 2 (Two Pointers):** We have one loop, and the `left` and `right` pointers will only ever visit each element *once*. This is a single pass over the array, making it $O(n)$. Both approaches use $O(1)$ space.

-----

## 🧩 8. Quick Test Cases

```python
sol = Solution()

# Example 1: Standard case
print(sol.maxArea([1, 8, 6, 2, 5, 4, 8, 3, 7]))
# ✅ Output: 49

# Example 2: Simple pair
print(sol.maxArea([1, 1]))
# ✅ Output: 1

# Example 3: Tall wall in middle
print(sol.maxArea([1, 2, 1]))
# ✅ Output: 2  (from [1, 2, 1] -> width=2, h=1, area=2)

# Example 4: Tallest walls are best
print(sol.maxArea([4, 3, 2, 1, 4]))
# ✅ Output: 16 (from [4, ..., 4] -> width=4, h=4, area=16)
```

-----

## 🧠 9. Summary Comparison

| Approach | Description | Time | Space | Best Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **1. Brute Force** | Check every single pair of lines with two nested loops. | $O(n^2)$ | $O(1)$ | Simple, but will time out. |
| **2. Two Pointers**| Start with max-width. Move the *shorter* pointer inward. | $O(n)$ | $O(1)$ | **Optimal solution.** |
