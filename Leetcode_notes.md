# leetcode-notes

# 📘 LeetCode & Data Structures Notes

Personal notes created while practicing **LeetCode-style problems**.  
Focused on **problem-solving process, time & space complexity, and clean Python solutions**.

---

## 🧠 Big-O Notation (Time & Space Complexity)

### Definitions
- **Time Complexity**: amount of time necessary to execute an algorithm
- **Space Complexity**: amount of memory necessary to execute an algorithm

Big-O measures how an algorithm scales as input size grows.

---

## 📈 Linear Big-O Example — `O(n)`

```python
def contains_two(nums):
    for num in nums:
        if num == 2:
            return True
        else:
            continue
    return False
````

Example input:

```python
[3, 10, 2, 7]
```

To loop through the entire list of `N` numbers and confirm whether `2` exists:

* Runtime grows as the list grows
* The longer the list, the longer it takes

**Time:** `O(n)`
**Space:** `O(1)`

---

## 📊 Big-O Reference Chart (Conceptual)

From fastest to slowest growth:

| Complexity   | Name         |
| ------------ | ------------ |
| `O(1)`       | Constant     |
| `O(log n)`   | Logarithmic  |
| `O(n)`       | Linear       |
| `O(n log n)` | Linearithmic |
| `O(n²)`      | Quadratic    |
| `O(2ⁿ)`      | Exponential  |
| `O(n!)`      | Factorial    |

As input size increases, algorithms with higher growth rates become impractical.

---

## 🧩 Problem-Solving Process (LeetCode)

Process I follow when solving problems:

1. Read the problem **twice**
2. Ask clarifying questions
3. Think of multiple ways to solve the problem
4. Think **end-to-end (E2E)** about the most efficient solution
5. Write the algorithm (often by drawing patterns)
6. Code the solution
7. Try to improve it once finished
8. Review other solutions (even if mine is correct)

---

## 📦 Arrays

Arrays store values in a fixed order and allow indexed access.
They are commonly used in interview problems.

---

## 🔁 Problem: Duplicate Values

### Problem

Given an integer array `nums`, return `true` if any value appears at least twice.
Return `false` if every element is distinct.

### Examples

```text
Input:  [1, 2, 3, 1]
Output: true

Input:  [1, 2, 3, 4]
Output: false

Input:  [1,1,1,3,3,4,3,2,4,2]
Output: true
```

### Constraints

* `1 <= nums.length <= 10^5`
* `-10^9 <= nums[i] <= 10^9`

---

### Naive Approach (Slow)

Loop through the list and compare elements.

* **Time:** `O(n²)` (quadratic)
* Too slow for large inputs

---

### Optimal Approach (Using a Set)

```python
def contains_duplicate(nums):
    if len(set(nums)) == len(nums):
        return False
    else:
        return True
```

* **Time:** `O(n)`
* **Space:** `O(n)`

---

### Notes on Python Sets

* Sets are a built-in data type
* Other collection types: **list, tuple, dictionary**
* **Unordered**: insertion order not preserved
* **Unchangeable**: elements themselves cannot be modified
* **Heterogeneous**: can store different data types
* **Unique**: duplicates are not allowed

Example:

```python
S = {20, "Jessa", 35.75}
```

Additional notes:

* Sets are fast
* Empty `{}` creates a dictionary, not a set
* Use `set()` for an empty set
* Implemented as a **hash table**
* Lookup / insert / delete: `O(1)` average

---

## ❓ Problem: Missing Number

### Problem

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the missing number.

---

### Examples

```text
Input:  [3, 0, 1]
Output: 2

Input:  [0, 1]
Output: 2

Input:  [9,6,4,2,3,5,7,0,1]
Output: 8
```

---

### Initial Solution (Sorting)

```python
nums.sort()
for i, v in enumerate(nums):
    if i != v:
        return v - 1
if v == len(nums) - 1:
    return v + 1
```

* Works correctly
* **But sorting makes it slow**
* **Time:** `O(n log n)`

---

### Better Solution (Math)

```python
def missing_number(nums):
    return sum(range(len(nums) + 1)) - sum(nums)
```

### Why This Works

* Expected sum of numbers `0 → n`
* Subtract actual sum of array
* Difference is the missing number

---

### Performance Notes

* `len()` → `O(1)`
* `range()` creation → `O(1)`
* `sum()` → `O(n)`
* `+1` needed because `range(n)` excludes `n`

---

````md
# 🧠 Sorting, Dictionaries & Hashing Notes

Practical notes and patterns for **sorting**, **lambda functions**, and **dictionary-based problem solving**, commonly used in **LeetCode and coding interviews**.

---

## 🔃 Dictionary Iteration

### Iterating Through a Dictionary
```python
for k, v in d.items():
    print(k, v)
````

Other common dictionary accessors:

```python
d.keys()    # returns all keys
d.values()  # returns all values
```

---

## 🔢 Sorting in Python

### `sorted()` Function

* Returns a **new sorted list**
* Does **not** modify the original iterable

```python
sorted(iterable, key=None, reverse=False)
```

### Sorting a Dictionary by Value

```python
print(sorted(x.items(), key=lambda y: y[1]))
```

* `x.items()` → returns `(key, value)` pairs
* `lambda y: y[1]` → sorts by value

---

### `.sort()` Method

```python
nums.sort()
```

* Works **only on lists**
* **No return value**
* Modifies the list **in-place**

---

## 🧩 Lambda Functions

### Syntax

```python
lambda arguments: expression
```

Example:

```python
lambda y: y[1]
```

Used frequently for:

* Sorting
* Key extraction
* One-line functions

---

## ❓ Problem: Find All Missing Numbers

### Problem

Given an array `nums` of length `n` where each number is in the range `[1, n]`, return **all numbers in that range that do not appear in `nums`**.

---

### Examples

```text
Input:  [4,3,2,7,8,2,3,1]
Output: [5,6]

Input:  [1,1]
Output: [2]
```

---

### Approach

1. Convert list to a set for fast lookup
2. Iterate through `range(1, n + 1)`
3. Append missing values to result list

---

### Solution

```python
def find_disappeared_numbers(nums):
    set_nums = set(nums)
    ret = []

    for i in range(1, len(nums) + 1):
        if i not in set_nums:
            ret.append(i)

    return ret
```

**Complexity**

* **Time:** `O(n)`
* **Space:** `O(n)`

---

## 🔢 Problem: Two Sum

### Problem

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers that add up to `target`.

* Exactly one solution exists
* Same element cannot be used twice
* Order does not matter

---

### Examples

```text
Input: nums = [2,7,11,15], target = 9
Output: [0,1]

Input: nums = [3,2,4], target = 6
Output: [1,2]

Input: nums = [3,3], target = 6
Output: [0,1]
```

---

## 📘 Dictionary Notes

* Dictionaries store data as **key-value pairs**
* **Unordered** (no index-based access)
* **Keys must be unique**
* **Mutable** (can add, update, or remove entries)

Example:

```python
d = {'a': 10, 'b': 20, 'c': 30}
```

---

## ✅ Optimal Two Sum Solution (Hash Map)

```python
def twoSum(nums: list[int], target: int) -> list[int]:
    hashMap = {}

    for index, value in enumerate(nums):
        complement = target - value

        if complement in hashMap:
            return [index, hashMap[complement]]

        hashMap[value] = index
```

### Why This Works

* Stores seen values in a dictionary
* Checks for the complement in `O(1)` time
* Finds solution in a single pass

**Complexity**

* **Time:** `O(n)`
* **Space:** `O(n)`

---

## 🎯 Key Takeaways

* Use **sets** for fast existence checks
* Use **dictionaries** to track values and indices
* Use **lambda functions** for concise sorting logic
* Prefer **hash-based solutions** over brute force


