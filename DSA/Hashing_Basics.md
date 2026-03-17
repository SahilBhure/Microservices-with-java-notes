

# 1. What is Hashing?

Hashing is a technique used to **store and retrieve data efficiently**.

---

### Core Idea

> Convert a key into an index using a function

---

### Example

```text id="p1v2hs"
Key → Hash Function → Index
 10 → hash() → 2
```

---

# 2. Why Hashing is Important

Without hashing:

* Searching = O(n)

With hashing:

* Searching = O(1) (average case)

---

### Real Interview Insight

> Many O(n²) problems become O(n) using hashing

---

# 3. HashMap (Key-Value Storage)

---

## What is HashMap?

Stores data in:

```text id="0p0f5x"
key → value
```

---

### Example

```java id="z5if07"
Map<Integer, String> map = new HashMap<>();

map.put(1, "A");
map.put(2, "B");

System.out.println(map.get(1)); // A
```

---

## Common Operations

| Operation     | Time Complexity |
| ------------- | --------------- |
| put()         | O(1)            |
| get()         | O(1)            |
| containsKey() | O(1)            |
| remove()      | O(1)            |

---

# 4. HashSet (Unique Elements)

---

## What is HashSet?

* Stores only keys
* No duplicates allowed

---

### Example

```java id="l4ax4y"
Set<Integer> set = new HashSet<>();

set.add(1);
set.add(2);
set.add(1); // ignored
```

---

### Use Case

> When you only care about **existence**

---

# 5. How Hashing Works Internally (Important)

---

## Step 1: Hash Function

Converts key → index

```text id="os33w3"
index = hash(key)
```

---

## Step 2: Bucket Storage

Data is stored in an array of buckets

---

## Step 3: Collision Handling

When two keys map to same index:

```text id="czkqcr"
key1 → index 2
key2 → index 2
```

---

### Collision Techniques

#### 1. Chaining

* Store multiple values in same bucket (linked list)

---

#### 2. Open Addressing (less common in Java)

---

# 6. Why HashMap is Not Always O(1)

Worst case:

* All elements collide → O(n)

---

### Java Optimization

* Converts linked list → balanced tree (after threshold)

---

# 7. When to Use HashMap

Use when:

* You need **fast lookup**
* You need to store relationships
* You need frequency counting

---

### Example: Frequency Count

```java id="odnpz4"
Map<Integer, Integer> freq = new HashMap<>();

for (int num : arr) {
    freq.put(num, freq.getOrDefault(num, 0) + 1);
}
```

---

# 8. When to Use HashSet

Use when:

* You only need to check duplicates
* You need uniqueness

---

# 9. Common Patterns Using Hashing

---

## Pattern 1: Lookup While Iterating

Used in:

* Two Sum

---

## Pattern 2: Frequency Counting

Used in:

* Most frequent element
* Anagram problems

---

## Pattern 3: Duplicate Detection

Used in:

* Contains duplicate

---

## Pattern 4: Complement Search

```text id="yepu7l"
target - current
```

Used in:

* Pair problems

---

# 10. Important Methods You Must Know

---

## HashMap

```java id="pj6x7m"
map.put(key, value);
map.get(key);
map.containsKey(key);
map.getOrDefault(key, defaultValue);
map.remove(key);
```

---

## HashSet

```java id="gq4q0b"
set.add(value);
set.contains(value);
set.remove(value);
```

---

# 11. Common Mistakes

---

## 1. Forgetting getOrDefault

```java id="dy80b5"
freq.put(num, freq.get(num) + 1); // error if null
```

---

## Correct

```java id="r5b9fh"
freq.put(num, freq.getOrDefault(num, 0) + 1);
```

---

## 2. Using HashMap When Not Needed

Sometimes:

> Simple array is enough

---

## 3. Ignoring Space Complexity

Hashing uses extra space O(n)

---

# 12. Interview Thinking

When you see:

* “Find pair”
* “Check duplicate”
* “Count frequency”
* “Find complement”

 Immediately think:

> “Can I use Hashing?”

---

# 13. Mental Model

Think of HashMap as:

```text id="8z9p3c"
Super fast dictionary
```

---

# 14. Key Takeaways

* Hashing = fast lookup
* Converts O(n²) → O(n)
* Essential for interviews
