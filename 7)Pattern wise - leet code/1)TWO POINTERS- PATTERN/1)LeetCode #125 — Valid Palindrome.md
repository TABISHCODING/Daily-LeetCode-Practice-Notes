

---

# 🧭 LeetCode #125 — Valid Palindrome

**Difficulty:** Easy | **Topic:** Strings | **Pattern:** Two Pointers

---

## 🧩 1. Problem Understanding (In Simple Words)

You’re given a **string `s`** that may contain:

* letters (A–Z, a–z)
* digits (0–9)
* spaces
* punctuation marks
* symbols

Your task:
👉 **Check if the string is a palindrome** —
that means it **reads the same forward and backward** —
**after** removing everything except letters and digits,
and ignoring case (uppercase vs lowercase doesn’t matter).

---

### ⚠️ Key Rules

| Rule                                   | Meaning                                              |
| -------------------------------------- | ---------------------------------------------------- |
| Remove all non-alphanumeric characters | Ignore spaces, punctuation, symbols, etc.            |
| Case-insensitive                       | ‘A’ == ‘a’                                           |
| Empty string → True                    | If nothing remains, treat as palindrome              |
| Only ASCII printable chars             | Input will be normal English letters/numbers/symbols |

---

### 💡 Example 1

```python
Input:  s = "A man, a plan, a canal: Panama"
Output: True
```

**Why:**
Clean string → `"amanaplanacanalpanama"`
Forward = Backward ✅

---

### 💡 Example 2

```python
Input:  s = "race a car"
Output: False
```

**Why:**
Clean string → `"raceacar"`
Forward = `"raceacar"`
Backward = `"rac a ecar"`
Not same ❌

---

### 💡 Example 3

```python
Input:  s = " "
Output: True
```

**Why:**
Clean string → `""` (empty)
Empty strings are palindromes ✅

---

## 🧠 2. Breaking Down the Problem

### What does “palindrome” mean?

> A sequence that reads the same from both ends.

For example:

```
"madam" → palindrome ✅
"apple" → not palindrome ❌
```

### What does “remove non-alphanumeric” mean?

Keep only:

* Letters (A–Z, a–z)
* Numbers (0–9)

Example:

```
Input: "A man, a plan, a canal: Panama"
After cleanup: "amanaplanacanalpanama"
```

---

## 🪜 3. Step-by-Step Approaches

---

### 🧩 Approach 1: **Brute Force (Clean + Reverse)**

---

#### 💡 Idea:

1. Build a **cleaned version** of the string that contains only lowercase letters/digits.
2. Compare it with its **reverse**.

If both are same → palindrome ✅
Otherwise → not palindrome ❌

---

#### 🧠 Step-by-step Thought Process:

1. Initialize an empty list `cleaned`.
2. For every character `c` in `s`:

   * If it’s alphanumeric (`c.isalnum()` is True),
     convert to lowercase (`c.lower()`) and append to `cleaned`.
3. Join everything into a new string.
4. Compare it with its reverse version.

---

#### 🧾 Code:

```python
def isPalindrome(s: str) -> bool:
    cleaned = []
    
    for c in s:
        if c.isalnum():           # keep only letters/numbers
            cleaned.append(c.lower())
    
    cleaned_str = ''.join(cleaned)
    return cleaned_str == cleaned_str[::-1]
```

---

#### 🧮 Example Walkthrough

Input:

```python
s = "A man, a plan, a canal: Panama"
```

| Step            | Character | Keep? | Cleaned List            |
| --------------- | --------- | ----- | ----------------------- |
| 1               | 'A'       | ✅ 'a' | ['a']                   |
| 2               | ' '       | ❌     | ['a']                   |
| 3               | 'm'       | ✅ 'm' | ['a','m']               |
| ...             | ...       | ...   | ...                     |
| → Final Cleaned |           |       | `amanaplanacanalpanama` |

Compare →
`cleaned_str == cleaned_str[::-1]` → ✅ True

Return `True`.

---

#### ⏱️ Complexity

| Metric | Complexity                  |
| ------ | --------------------------- |
| Time   | O(n) — one pass + reverse   |
| Space  | O(n) — store cleaned string |

✅ Easy to write
❌ Slightly more memory usage (O(n))

---

### ⚡ Approach 2: **Two Pointer (Optimal, O(1) Extra Space)**

---

#### 💡 Core Idea

Instead of building a new string,
→ use **two pointers** (`left`, `right`)
→ move inward from both ends
→ skip any non-alphanumeric characters
→ compare characters (case-insensitive).

If all matching → palindrome ✅
If any mismatch → False ❌

---

#### 🧠 Step-by-Step Thought Process

1. Initialize:

   ```python
   left = 0
   right = len(s) - 1
   ```

2. While `left < right`:

   * Skip invalid characters:

     ```python
     while left < right and not s[left].isalnum():
         left += 1
     while left < right and not s[right].isalnum():
         right -= 1
     ```
   * Compare lowercase versions:

     ```python
     if s[left].lower() != s[right].lower():
         return False
     ```
   * Move pointers inward:

     ```python
     left += 1
     right -= 1
     ```

3. If loop finishes → all matches ✅ → return `True`.

---

#### 🧾 Code

```python
def isPalindrome(s: str) -> bool:
    left, right = 0, len(s) - 1

    while left < right:
        # move left pointer to next alphanumeric
        while left < right and not s[left].isalnum():
            left += 1
        # move right pointer to previous alphanumeric
        while left < right and not s[right].isalnum():
            right -= 1

        # compare case-insensitively
        if s[left].lower() != s[right].lower():
            return False

        left += 1
        right -= 1

    return True
```

---

#### 🧮 Example Walkthrough

Input:

```python
s = "A man, a plan, a canal: Panama"
```

| Step          | left | right | s[left] | s[right] | Action         |
| ------------- | ---- | ----- | ------- | -------- | -------------- |
| 1             | 0    | 29    | 'A'     | 'a'      | match ✅        |
| 2             | 1    | 28    | ' '     | ':'      | skip non-alnum |
| 3             | 2    | 27    | 'm'     | 'm'      | match ✅        |
| ...           | ...  | ...   | ...     | ...      |                |
| ✅ All matched |      |       |         |          | Return True    |

---

#### ⏱️ Complexity

| Metric | Complexity           |
| ------ | -------------------- |
| Time   | O(n) — scan once     |
| Space  | O(1) — only pointers |

✅ Very efficient
✅ No extra string created
✅ Perfect for interview use

---

## ⚙️ 4. Edge Cases

| Input   | Explanation                       | Output  |
| ------- | --------------------------------- | ------- |
| `" "`   | Empty after cleaning → palindrome | `True`  |
| `"0P"`  | `'0'` ≠ `'p'`                     | `False` |
| `"aa"`  | `'a'` == `'a'`                    | `True`  |
| `"a"`   | Single char → palindrome          | `True`  |
| `"!!!"` | No alnum → empty → palindrome     | `True`  |

---

## 🧠 5. Why “Two Pointers” Pattern Fits Perfectly

| Trigger Word              | Meaning                     | Why Two Pointers?          |
| ------------------------- | --------------------------- | -------------------------- |
| “Compare from both ends”  | Check start & end of string | ✅ Two pointers             |
| “Ignore non-alphanumeric” | Need skipping logic         | ✅ Easy with pointers       |
| “Palindrome”              | Symmetry around center      | ✅ Classic two-pointer case |

So whenever you see these **keywords**:
👉 *“compare from both ends”*, *“palindrome”*, or *“string symmetry”*,
think **Two Pointer pattern**!

---

## ✅ Final Summary

| Approach                | Time | Space | Key Idea                               | Use When            |
| ----------------------- | ---- | ----- | -------------------------------------- | ------------------- |
| Clean + Reverse (Brute) | O(n) | O(n)  | Build new clean string and compare     | Simpler to code     |
| Two Pointers (Optimal)  | O(n) | O(1)  | Skip & compare directly from both ends | Best for interviews |

---

### 💡 Final Best Code

```python
def isPalindrome(s: str) -> bool:
    left, right = 0, len(s) - 1

    while left < right:
        while left < right and not s[left].isalnum():
            left += 1
        while left < right and not s[right].isalnum():
            right -= 1

        if s[left].lower() != s[right].lower():
            return False

        left += 1
        right -= 1

    return True
```

---

### 🧩 What You Learned from This Question

✅ How to clean and normalize string inputs
✅ The concept of palindrome checking
✅ Why “compare from both ends” = **Two Pointer pattern**
✅ How skipping logic works with non-alphanumeric characters
✅ Trade-offs between brute force and optimal approach

---


