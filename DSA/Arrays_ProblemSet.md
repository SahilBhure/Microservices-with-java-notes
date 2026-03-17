

# Problem 1: Two Sum

---

## Problem Statement

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to target.

---

## Example

```text
nums = [2, 7, 11, 15]
target = 9

Output: [0, 1]
```

---

## Step 1: Brute Force Thinking

> Try all pairs

---

### Approach

* Pick one element
* Compare with all other elements

---

### Code

```java
int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) {
                return new int[]{i, j};
            }
        }
    }
    return new int[]{};
}
```

---

### Time Complexity

O(n²)

---

### Key Insight

> This is the default thinking when no optimization is known

---

## Step 2: Better Thinking

Ask:

> “Am I repeating work?”

Yes.

For every element, we search again.

---

## Step 3: Optimal Solution (HashMap)

---

### Core Idea

Instead of searching:

> Store elements while iterating

---

### Logic

* For each element `x`
* Check if `target - x` already exists

---

### Code

```java
int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();

    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];

        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }

        map.put(nums[i], i);
    }
    return new int[]{};
}
```

---

### Time Complexity

O(n)

---

### Space Complexity

O(n)

---

### Pattern Learned

> “Lookup while iterating”

This is one of the **most important patterns in DSA**

---

# Problem 2: Find Maximum Element

---

## Problem Statement

Find the largest element in the array.

---

## Brute Force (Also Optimal)

---

### Code

```java
int max = arr[0];

for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}
```

---

### Time Complexity

O(n)

---

### Insight

> Sometimes brute force is already optimal

---

# Problem 3: Contains Duplicate

---

## Problem Statement

Return true if any value appears at least twice.

---

## Example

```text
[1, 2, 3, 1] → true
[1, 2, 3, 4] → false
```

---

## Brute Force

---

### Code

```java
for (int i = 0; i < nums.length; i++) {
    for (int j = i + 1; j < nums.length; j++) {
        if (nums[i] == nums[j]) {
            return true;
        }
    }
}
return false;
```

---

### Time Complexity

O(n²)

---

## Optimal Solution (HashSet)

---

### Idea

* Store elements
* If already exists → duplicate

---

### Code

```java
Set<Integer> set = new HashSet<>();

for (int num : nums) {
    if (set.contains(num)) {
        return true;
    }
    set.add(num);
}
return false;
```

---

### Time Complexity

O(n)

---

### Pattern Learned

> “Use HashSet for existence checking”

---

# Problem 4: Reverse an Array

---

## Problem Statement

Reverse the array in-place.

---

## Approach

Swap elements from both ends

---

### Code

```java
int left = 0;
int right = arr.length - 1;

while (left < right) {
    int temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;

    left++;
    right--;
}
```

---

### Time Complexity

O(n)

---

### Pattern Learned

> “Two Pointer Technique (intro)”

---

# Problem 5: Sum of All Elements

---

## Code

```java
int sum = 0;

for (int num : arr) {
    sum += num;
}
```

---

### Time Complexity

O(n)

---

### Pattern Learned

> “Running Sum”

---

# Key Patterns You Learned in This File

---

## 1. Brute Force (Nested Loops)

* Try all possibilities
* Usually O(n²)

---

## 2. Hashing (VERY IMPORTANT)

* HashMap → key-value lookup
* HashSet → existence check

---

## 3. Two Pointers (Intro)

* Used for reversing
* Will be used heavily later

---

## 4. Running Variables

* sum
* max
* min

---

# How to Practice This File

---

## You MUST:

1. Code all problems yourself
2. Do not copy-paste
3. Dry run with example
4. Re-code without seeing

