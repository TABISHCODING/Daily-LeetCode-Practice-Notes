
---

# 🧩 **LeetCode 125. Valid Palindrome — Complete Structured Notes**

---

## 🧠 1. Problem Understanding (Simplified)

You are given a **string `s`** that may contain:

* Letters (`A–Z`, `a–z`)
* Digits (`0–9`)
* Spaces, punctuation, symbols, etc.

✅ **Goal:**
Check if the string is a **palindrome** —
reads the same forward and backward —
**after removing all non-alphanumeric characters** and **ignoring case**.

---

### ⚙️ Example 1

```python
Input:  s = "A man, a plan, a canal: Panama"
Output: True
```

**Why:**
After cleaning → `"amanaplanacanalpanama"`
Same forward and backward ✅

---

### ⚙️ Example 2

```python
Input:  s = "race a car"
Output: False
```

**Why:**
After cleaning → `"raceacar"`
Forward ≠ Backward ❌

---

### ⚙️ Example 3

```python
Input:  s = " "
Output: True
```

**Why:**
After cleaning → `""` (empty string)
An empty string is considered palindrome ✅

---

## 🧩 2. Approach 1 — Brute Force (Clean + Reverse Compare)

---

### 💡 Idea

1. Build a **cleaned version** of the string keeping only alphanumeric characters.
2. Convert all to lowercase.
3. Compare cleaned string with its reverse:

   * Same → palindrome ✅
   * Different → not palindrome ❌

---

### ⏱️ Time Complexity: O(n)

### 💾 Space Complexity: O(n)

---

### 🧾 Code — Brute Force

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # 1️⃣ Build a cleaned string with only alphanumeric characters (a–z, 0–9)
        clean = ""
        for ch in s:
            if ch.isalnum():          # Keep only letters and digits
                clean += ch.lower()   # Convert to lowercase and add to 'clean'
        
        # 2️⃣ Compare cleaned string with its reverse
        return clean == clean[::-1]
```

---

### 🧮 Dry Run — `"A man, a plan, a canal: Panama"`

| Step | ch  | ch.isalnum()? | Action  | clean                     |
| ---- | --- | ------------- | ------- | ------------------------- |
| 1    | 'A' | ✅             | Add 'a' | `"a"`                     |
| 2    | ' ' | ❌             | Skip    | `"a"`                     |
| 3    | 'm' | ✅             | Add 'm' | `"am"`                    |
| 4    | 'a' | ✅             | Add 'a' | `"ama"`                   |
| ...  | ... | ...           | ...     | ...                       |
| ✅    | —   | —             | —       | `"amanaplanacanalpanama"` |

Now check:

```
clean == clean[::-1] ✅
```

→ **Return True**

---

### ✅ Advantages

* Simple and clear for beginners.

### ⚠️ Limitations

* Uses extra O(n) space to store cleaned string.

---

## 🧩 3. Approach 2 — Two Pointer (Optimal, O(1) Space)

---

### 💡 Idea

Use **two pointers** —
`left` starts at beginning, `right` starts at end.

1. Move both pointers toward the center.
2. Skip all non-alphanumeric characters.
3. Compare lowercase versions of characters.
4. If mismatch → return False.
5. If loop ends → palindrome ✅

---

### ⏱️ Time Complexity: O(n)

### 💾 Space Complexity: O(1)

---

### 🧾 Code — Two Pointer Approach

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Initialize pointers
        left, right = 0, len(s) - 1

        # Loop until pointers meet
        while left < right:

            # 1️⃣ Skip non-alphanumeric characters from the left
            while left < right and not s[left].isalnum():
                left += 1  # move left pointer forward until a valid char

            # 2️⃣ Skip non-alphanumeric characters from the right
            while left < right and not s[right].isalnum():
                right -= 1  # move right pointer backward until valid char

            # 3️⃣ Compare lowercase versions of both characters
            if s[left].lower() != s[right].lower():
                return False  # ❌ mismatch found

            # 4️⃣ Move inward if match
            left += 1
            right -= 1

        # ✅ If loop completes, all chars matched
        return True
```

---

## 🔍 Deep Dive — How the “Skip” Works

These two lines:

```python
while left < right and not s[left].isalnum():
    left += 1

while left < right and not s[right].isalnum():
    right -= 1
```

mean:

> “Keep moving pointers inward until you find a letter or digit.”

This helps **ignore spaces, commas, punctuation, etc.**

---

## 🧮 Step-by-Step Dry Run (Detailed)

🎯 **Input:**

```python
s = "A man, a plan, a canal: Panama"
```

Goal → check palindrome ignoring spaces, commas, and colon.

---

### ⚙️ Setup

```python
left = 0
right = len(s) - 1  # 29
```

So initially:

```
s[left] = 'A'
s[right] = 'a'
```

---

### 🔍 Step-by-Step Execution

| Step | left | right | s[left] | s[right] | Action / Condition               | Result            |
| ---- | ---- | ----- | ------- | -------- | -------------------------------- | ----------------- |
| 1    | 0    | 29    | 'A'     | 'a'      | Both alphanumeric ✅ → Compare    | 'A' == 'a' ✅      |
|      |      |       |         |          | Move inward → left=1, right=28   |                   |
| 2    | 1    | 28    | `' '`   | `'m'`    | `' '` is not alnum ❌ → Skip left | left=2            |
| 3    | 2    | 28    | `'m'`   | `'m'`    | Match ✅                          | left=3, right=27  |
| 4    | 3    | 27    | `'a'`   | `'a'`    | Match ✅                          | left=4, right=26  |
| 5    | 4    | 26    | `'n'`   | `'n'`    | Match ✅                          | left=5, right=25  |
| 6    | 5    | 25    | `','`   | `'a'`    | `','` not alnum ❌ → Skip left    | left=6            |
| 7    | 6    | 25    | `' '`   | `'a'`    | `' '` not alnum ❌ → Skip left    | left=7            |
| 8    | 7    | 25    | `'a'`   | `'a'`    | Match ✅                          | left=8, right=24  |
| 9    | 8    | 24    | `' '`   | `'P'`    | `' '` not alnum ❌ → Skip left    | left=9            |
| 10   | 9    | 24    | `'p'`   | `'P'`    | Match ✅ (case-insensitive)       | left=10, right=23 |
| ...  | ...  | ...   | ...     | ...      | Continue pattern till center     | ...               |
| ✅    | —    | —     | —       | —        | All matched                      | Return True ✅     |

---

### 🧩 Visualization of the Skip Logic

```
Original:  A   _   m   a   n ,   _   a   _   p   l   a   n ,   _   a   ...
Pointers:  ^                                   ^

Step 1: Compare → A == a ✅
Step 2: Skip spaces and commas → pointers move to letters only
Step 3: Compare inward until all match
✅ Result: True
```

---

### ✅ Advantages

* No extra memory needed.
* Directly processes the original string.
* Fast and efficient for large text inputs.

---

## 🧩 4. Quick Test Cases

```python
sol = Solution()

print(sol.isPalindrome("A man, a plan, a canal: Panama"))  # ✅ True
print(sol.isPalindrome("race a car"))                      # ❌ False
print(sol.isPalindrome(" "))                               # ✅ True
print(sol.isPalindrome("0P"))                              # ❌ False
print(sol.isPalindrome("aa"))                              # ✅ True
print(sol.isPalindrome("a"))                               # ✅ True
print(sol.isPalindrome("!!!"))                             # ✅ True
```

---

## 🏁 Output

```
True
False
True
False
True
True
True
```

---

## 🧠 Summary Comparison

| Approach           | Method                  | Time | Space | Description                |
| ------------------ | ----------------------- | ---- | ----- | -------------------------- |
| **1. Brute Force** | Clean + Reverse Compare | O(n) | O(n)  | Simple & beginner-friendly |
| **2. Two Pointer** | In-place, Skip Symbols  | O(n) | O(1)  | Optimal and efficient      |

---


