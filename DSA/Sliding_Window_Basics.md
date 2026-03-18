
# 1. What is Sliding Window?

Sliding Window is an optimized technique to handle **subarrays / substrings**.

---

### Core Idea

Instead of:

* Generating all subarrays (O(n²) or O(n³))

We:

> Maintain a “window” and slide it → O(n)

---

# 2. Why Sliding Window is Important

* Reduces complexity drastically
* Used in many real interview problems
* Builds on Two Pointers

---

### Real Insight

> If problem says “subarray” or “substring” → think Sliding Window

---

# 3. Types of Sliding Window

---

## Type 1: Fixed Size Window

Window size is constant

---

### Example

Find max sum of subarray of size k

---

## Type 2: Variable Size Window (More Important)

Window expands and shrinks dynamically

---

### Example

Longest substring without repeating characters

---

# 4. Fixed Size Window (Concept)

---

## Example Problem

Find max sum of subarray of size k

---

### Brute Force

```text
Try all subarrays of size k → O(n*k)
```

---

## Optimal Sliding Window

---

### Idea

* Add next element
* Remove previous element

---

### Code

```java id="i8w7b4"
int maxSum = 0;
int windowSum = 0;
int k = 3;

// first window
for (int i = 0; i < k; i++) {
    windowSum += arr[i];
}
maxSum = windowSum;

// slide window
for (int i = k; i < arr.length; i++) {
    windowSum += arr[i];       // add new
    windowSum -= arr[i - k];   // remove old
    maxSum = Math.max(maxSum, windowSum);
}
```

---

### Time Complexity

O(n)

---

### Pattern

> Add next, remove previous

---

# 5. Variable Size Window (Core Concept)

---

## Structure

```java
int left = 0;

for (int right = 0; right < n; right++) {

    // expand window

    while (condition not satisfied) {
        // shrink window
        left++;
    }

    // update answer
}
```

---

### Key Idea

* Expand → include elements
* Shrink → remove unwanted elements

---

# 6. Example: Longest Substring Without Repeating

---

### Already Seen

Uses:

* Set
* Expand right
* Shrink left

---

### Pattern

> Expand → check → shrink → update

---

# 7. When to Use Sliding Window

---

## Signals

* Subarray / substring
* Contiguous elements
* Maximum / minimum length
* Count of valid windows

---

# 8. Sliding Window vs Two Pointers

---

## Two Pointers

* General technique

---

## Sliding Window

* Special case of two pointers
* Focus on contiguous range

---

# 9. Common Patterns

---

## Pattern 1: Fixed Size

* Window size = k
* Move window

---

## Pattern 2: Expand & Shrink

* Use while loop to shrink

---

## Pattern 3: Condition Based

* Maintain validity (unique, sum, etc.)

---

# 10. Common Mistakes

---

## 1. Forgetting to shrink ❌

Leads to wrong results

---

## 2. Not updating answer at correct time ❌

---

## 3. Using nested loops unnecessarily ❌

---

# 11. Mental Model

Think of sliding window as:

```text
A moving frame over array
```

---

# 12. Step-by-Step Thinking

When you see a problem:

---

### Step 1

Is it subarray / substring?

---

### Step 2

Can I avoid recomputing values?

---

### Step 3

Can I reuse previous computation?

---

👉 If yes → Sliding Window

---

# 13. Key Takeaways

* Converts O(n²) → O(n)
* Works on contiguous elements
* Uses left & right pointers
* Requires careful condition handling

