
# 1. What is Binary Search?

Binary Search is an algorithm used to **search efficiently in a sorted array**.

---

### Core Idea

> Divide the search space in half every time

---

### Instead of:

* Linear search → O(n)

We use:

> Binary Search → O(log n)

---

# 2. Why Binary Search is Powerful

Each step:

* Eliminates half of the elements

---

### Example

```text id="x1t3e9"
Array size = 1000

Step 1 → 500 left  
Step 2 → 250  
Step 3 → 125  
...
```

---

### Insight

> Very fast for large data

---

# 3. Basic Binary Search (Classic)

---

## Problem

Find target in sorted array

---

## Logic

1. Find middle
2. Compare with target
3. Move left or right

---

## Code

```java id="p6w7ob"
int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return -1;
}
```

---

### Time Complexity

O(log n)

---

# 4. Important Detail: Mid Calculation

---

## Wrong (can overflow)

```java id="rmeixy"
int mid = (left + right) / 2;
```

---

## Correct

```java id="z4pnqz"
int mid = left + (right - left) / 2;
```

---

# 5. Binary Search Variations (VERY IMPORTANT)

---

## 1. First Occurrence

Find first position of target

---

## 2. Last Occurrence

Find last position

---

## 3. Lower Bound

First element ≥ target

---

## 4. Upper Bound

First element > target

---

### These are asked VERY frequently

---

# 6. When to Use Binary Search

---

## Signals

* Sorted array
* “Search” problem
* Find position/index
* Reduce search space

---

# 7. Binary Search on Answer (ADVANCED)

---

## Most Important Concept

Sometimes:

> You don’t search element
> You search the **answer**

---

## Example Thinking

Instead of:

* Finding exact value

You:

* Guess answer
* Check if valid

---

### Pattern

```text id="vax3q4"
low = minimum possible answer  
high = maximum possible answer  

while (low <= high):
    mid = (low + high) / 2
    
    if (mid is valid):
        move left (try better)
    else:
        move right
```

---

# 8. Example: Guessing Answer

---

## Problem Idea

Minimum speed to finish tasks

---

### Thinking

* Try speed = mid
* If possible → try smaller
* Else → increase

---

### Pattern Learned

> Binary search on answer space

---

# 9. Common Mistakes

---

## 1. Using on Unsorted Array 

Binary search requires:

> Sorted data

---

## 2. Infinite Loop 

Wrong condition:

```java
while (left < right)
```

Correct:

```java
while (left <= right)
```

---

## 3. Wrong Pointer Movement 

Must do:

```java
left = mid + 1  
right = mid - 1
```

---

# 10. Mental Model

Think of binary search as:

```text id="5y9mlp"
Cutting the search space in half
```

---

# 11. Pattern Summary

---

## Classic Binary Search

Find element

---

## Bound Search

Find first/last occurrence

---

## Answer Search

Search possible answers

---

# 12. Interview Thinking

When you see:

* Sorted array
* “Find position”
* “Minimum/maximum possible value”

Think:

> Binary Search

---

# 13. Key Takeaways

* O(log n) efficiency
* Works on sorted data
* Has multiple variations
* Binary search on answer is very powerful

