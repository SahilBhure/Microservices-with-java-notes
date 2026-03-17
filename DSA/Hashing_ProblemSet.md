
# Problem 1: Valid Anagram

---

## Problem Statement

Given two strings `s` and `t`, return true if `t` is an anagram of `s`.

---

## Example

```text
s = "anagram", t = "nagaram" → true  
s = "rat", t = "car" → false
```

---

## Step 1: Brute Force Thinking

---

### Idea

* Sort both strings
* Compare them

---

### Code

```java
boolean isAnagram(String s, String t) {
    char[] a = s.toCharArray();
    char[] b = t.toCharArray();

    Arrays.sort(a);
    Arrays.sort(b);

    return Arrays.equals(a, b);
}
```

---

### Time Complexity

O(n log n)

---

## Step 2: Optimal (Frequency Count using HashMap)

---

### Idea

* Count frequency of each character
* Compare both

---

### Code

```java
boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;

    Map<Character, Integer> map = new HashMap<>();

    for (char c : s.toCharArray()) {
        map.put(c, map.getOrDefault(c, 0) + 1);
    }

    for (char c : t.toCharArray()) {
        if (!map.containsKey(c) || map.get(c) == 0) {
            return false;
        }
        map.put(c, map.get(c) - 1);
    }

    return true;
}
```

---

### Time Complexity

O(n)

---

### Pattern Learned

> Frequency counting

---

# Problem 2: First Non-Repeating Character

---

## Problem Statement

Find the first character that appears only once.

---

## Example

```text
"leetcode" → 'l'  
"aabb" → none
```

---

## Approach

---

### Step 1: Count frequency

### Step 2: Traverse again

---

### Code

```java
char firstUnique(String s) {
    Map<Character, Integer> map = new HashMap<>();

    for (char c : s.toCharArray()) {
        map.put(c, map.getOrDefault(c, 0) + 1);
    }

    for (char c : s.toCharArray()) {
        if (map.get(c) == 1) {
            return c;
        }
    }

    return '_';
}
```

---

### Time Complexity

O(n)

---

### Pattern Learned

> Two-pass Hashing

---

# Problem 3: Longest Substring Without Repeating Characters

---

## Problem Statement

Find length of longest substring without repeating characters.

---

## Example

```text
"abcabcbb" → 3 ("abc")
```

---

## Step 1: Brute Force

---

### Idea

* Generate all substrings
* Check uniqueness

---

### Complexity

O(n³)

---

## Step 2: Better (Using Set + Sliding Window)

---

### Idea

* Maintain window with unique characters
* Expand and shrink

---

### Code

```java
int lengthOfLongestSubstring(String s) {
    Set<Character> set = new HashSet<>();
    int left = 0, maxLength = 0;

    for (int right = 0; right < s.length(); right++) {
        while (set.contains(s.charAt(right))) {
            set.remove(s.charAt(left));
            left++;
        }

        set.add(s.charAt(right));
        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```

---

### Time Complexity

O(n)

---

### Pattern Learned

> Sliding Window + HashSet

---

# Problem 4: Intersection of Two Arrays

---

## Problem Statement

Return intersection of two arrays (unique elements).

---

## Example

```text
nums1 = [1,2,2,1]
nums2 = [2,2]

Output: [2]
```

---

## Approach (HashSet)

---

### Code

```java
int[] intersection(int[] nums1, int[] nums2) {
    Set<Integer> set1 = new HashSet<>();
    Set<Integer> result = new HashSet<>();

    for (int num : nums1) {
        set1.add(num);
    }

    for (int num : nums2) {
        if (set1.contains(num)) {
            result.add(num);
        }
    }

    return result.stream().mapToInt(Integer::intValue).toArray();
}
```

---

### Time Complexity

O(n + m)

---

### Pattern Learned

> Set intersection

---

# Problem 5: Frequency of Elements

---

## Problem Statement

Count frequency of each element in array.

---

### Code

```java
Map<Integer, Integer> freq = new HashMap<>();

for (int num : arr) {
    freq.put(num, freq.getOrDefault(num, 0) + 1);
}
```

---

### Output Example

```text
[1,1,2,3,3,3]

→ {1=2, 2=1, 3=3}
```

---

### Pattern Learned

> Frequency Map

---

# Key Patterns You Learned

---

## 1. Frequency Counting

* Anagram
* Counting elements

---

## 2. Two-Pass Hashing

* First pass → build data
* Second pass → answer

---

## 3. Sliding Window + Hashing

* Longest substring
* Unique constraints

---

## 4. Set Operations

* Intersection
* Duplicate detection

---

# Important Interview Signals

When you see:

* “Anagram” → Frequency count
* “Unique substring” → Sliding window
* “Duplicate” → HashSet
* “Count occurrences” → HashMap

---

# What You Should Do Now

---

## Practice

Re-code all problems:

* Without seeing solution
* Explain logic out loud

---

## Focus

Don’t memorize code.

> Understand WHY each approach works

