
---

# 🧩 **LeetCode 9 — Palindrome Number (Complete Structured Notes)**

---

## 🧠 1. Problem Understanding

Given an integer `x`, determine whether it **reads the same forward and backward**.

A **palindrome number** remains identical even when its digits are reversed.

---

### ⚙️ Examples

| Input  | Explanation                             | Output  |
| :----- | :-------------------------------------- | :------ |
| `121`  | `121` reversed = `121`                  | ✅ True  |
| `-121` | Negative → `121-` ≠ `-121`              | ❌ False |
| `10`   | Reversed = `01` → leading 0 not allowed | ❌ False |

---

## 🥉 1️⃣ Brute Force — String Conversion + Reverse Compare

### 💡 Idea

1. Convert the integer into a string.
2. Reverse the string.
3. Compare original vs reversed.

---

### 💾 Code

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        s = str(x)
        return s == s[::-1]
```

---

### 🧮 Dry Run Example

**Input:** `x = 121`

| Step    | Expression       | Result  |
| ------- | ---------------- | ------- |
| Convert | `str(x)`         | `"121"` |
| Reverse | `"121"[::-1]`    | `"121"` |
| Compare | `"121" == "121"` | ✅ True  |

**Input:** `x = -121` → `"-121" != "121-"` → ❌ False

---

### 📊 Complexity

| Type  | Value                    |
| :---- | :----------------------- |
| Time  | O(n) — n = digits count  |
| Space | O(n) — string conversion |

---

## 🥈 2️⃣ Two Pointer Approach (String Version)

### 💡 Idea

1. Convert to string `s`.
2. Use **two pointers** (`left`, `right`).
3. Compare `s[left]` and `s[right]` until middle.
4. Any mismatch → False.

---

### 💾 Code

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        s = str(x)
        left, right = 0, len(s) - 1
        while left < right:
            if s[left] != s[right]:
                return False
            left += 1
            right -= 1
        return True
```

---

### 🧮 Dry Run Example

**Input:** `x = 12321`

| Step | left | right | s[left] | s[right] | Action              | Result |
| ---- | :--: | :---: | :-----: | :------: | :------------------ | :----- |
| 1    |   0  |   4   |    1    |     1    | Match → move inward | ✅      |
| 2    |   1  |   3   |    2    |     2    | Match → move inward | ✅      |
| 3    |   2  |   2   |    3    |     3    | Center met          | ✅      |
|      |   —  |   —   |    —    |     —    | All matched → True  | ✅      |

---

### 📊 Complexity

| Type  | Value                    |
| :---- | :----------------------- |
| Time  | O(n)                     |
| Space | O(n) (string conversion) |

---

## 🥇 3️⃣ Optimal Approach — No String Conversion (O(1) Space)

### 💡 Core Idea

Work purely with numbers:

1. Negative → not palindrome ❌
2. Numbers ending in 0 (but not 0 itself) → not palindrome ❌
3. Reverse **half** of the digits and compare halves.

---

### 💾 Code

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        # 1️⃣ Quick rejections
        if x < 0 or (x % 10 == 0 and x != 0):
            return False

        rev = 0
        # 2️⃣ Reverse half
        while x > rev:
            rev = rev * 10 + x % 10
            x //= 10

        # 3️⃣ Compare halves
        return x == rev or x == rev // 10
```

---

### 🧮 Step-by-Step Dry Run

**Input:** `x = 12321`

| Iter | x (before) | rev (before) | Action (`rev = rev*10 + x%10`) | x (after) | rev (after) |
| :--: | :--------- | :----------- | :----------------------------- | :-------- | :---------- |
|   1  | 12321      | 0            | `0*10+1`                       | 1232      | 1           |
|   2  | 1232       | 1            | `1*10+2`                       | 123       | 12          |
|   3  | 123        | 12           | `12*10+3`                      | 12        | 123         |
|      | 12         | 123          | Loop stops (x < rev)           | —         | —           |

Now check:

```
x == rev // 10
12 == 123 // 10 → 12 == 12 ✅
```

✅ Palindrome

---

### 🧩 Complexity Summary

| Approach                        | Time     | Space | Notes              |
| :------------------------------ | :------- | :---- | :----------------- |
| 🥇 Reverse Half Number          | O(log n) | O(1)  | Optimal, no string |
| 🥈 Two Pointer (String)         | O(n)     | O(n)  | Clean & simple     |
| 🥉 Brute Force (String Reverse) | O(n)     | O(n)  | Basic method       |

---

## 🧠 Key Takeaways

✅ **Negative numbers** → always False
✅ **Trailing 0** → False unless `x == 0`
✅ Optimal method avoids string conversion → O(1) space
✅ Concept similar to string palindrome but digit-based

---


