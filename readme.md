# hashMap

- " HashMap is a collection that stores key-value pairs."
- "the hashMap works liek this 
first it's take a key and value but the key mmust be unique abd to store it here where iis hashCode comes it's take the key and then provide hashChode and he devide it by the number of "buckets" or "slots" and it give you the index
like this [1,2,3,4] 
then we wanna to store {key:"mustapha" , value:"24"}
it will take key and hash it so we got 8 and we take the modulo of it with length of Arr which is 4 and  8%4 = 0 so this data we put it in the index 0 

but what is the modulo?
modulo is the remainder of a division
Example:
8 ÷ 4 = 2 with a remainder of 0
8 % 4 = 0

Note: there is a big diffreence between devision and modulo 
Problem: what if the hashcode of two different keys are the same?
Here where java use Collision "it's like saying ok they have the same hachcode so we put them in the same bucket"

but how ?
- Before java 8: it's use a linked list -->but that's make it slow
- After java 8: it's use tree

# hash
### kepp in mind: -Important
- why the String key is good:
"it's because is  immutable so it's unique "
- string builder not good as a key because t's mutable  "it's like saying i have 2 different keys but they are the same"


Note: the hashMap is not thread-safe we can write in it at the same time from diffrent threads it will cause a collision it will make a mess 



# ConcurrentHashMap (hashMap multithreading):

### conclusion 
“HashMap stores data in buckets using hashCode.
Collisions happen when multiple keys go to the same bucket.”

ok let's say that we have a hashMap and we wanna to get a bucket value
so here if in collision case we have two diffrent key but with the same hashCode so here we must use "Equals" to check,so the hashMap based on the hashCode() and Equals()
and note: ovveriding equals over hashCode is may cause issue !! why:
because if we use just equals that gonna code O(n) because we have to check every bucket and it's value

so summary:
hashCode → reduces search space (find bucket)
equals   → finds exact key inside bucket


# important
### resizing
capacity: the default capacity is 16 (and it's the number of buckets)
load factor : the default load factor is 0.75
size: number of elements in the hashMap
and resizing happen when size > loadFactor * capacity


### concurrent hashMap (thread safe):
before java 8: it's use segment 
after java 8: it's use CAS (Compare and Swap) + Lock Striping
CAS: 
1 - thread A chekc the value if it's the same as before so it replace it if its diffrent so it reject 
2 - thread B chekc the value if it's the same before replace it if it's no like in this case reject and retry


# hashmap vs treemap

| Feature             | HashMap                                          | TreeMap                              |
| ------------------- | ------------------------------------------------ | ------------------------------------ |
| ** Underlying DS** | Hash table (buckets + linked list/tree)           | Balanced Binary Search Tree          |
| ** Ordering**        | No guaranteed order                              | Sorted order (natural or comparator) |
| **Performance**     | Average O(1) for put/get                        | O(log n) for put/get                 |
| **Null Keys**       | Allows one null key                              | Does NOT allow null keys             |
| **Thread Safety**   | Not thread-safe                                  | Not thread-safe                      |
| **Best For**        | Fast lookups when order doesn’t matter           | Sorted data, range queries           |


# hashmap vs linkedhashmap

| Feature             | HashMap                                          | LinkedHashMap                         |
| ------------------- | ------------------------------------------------ | ------------------------------------- |
| ** Underlying DS** | Hash table                                       | Hash table + Doubly Linked List       |
| **Ordering**        | No guaranteed order                              | Insertion order preserved             |
| **Performance**     | Average O(1)                                     | Average O(1)                          |
| **Null Keys**       | Allows one null key                              | Allows one null key                   |
| **Thread Safety**   | Not thread-safe                                  | Not thread-safe                       |
| **Memory Overhead** | Lower                                            | Slightly higher (due to next/prev)    |
| **Use Case**        | Unordered key-value storage                      | Ordered caches, history, FIFO         |



# collections in java:
- List
- Set
- Map(not form the collections interface)
ArrayList / linkedList 
HashSet / linkedHashSet / treeSet
HashMap / linkedHashMap / treeMap
Set: it's a collection that doens't allow the duplicate items
List: it's a collection that allow the duplicate items and insertion order
Map: it's a collection that stores key-value pairs
TreeSet: it's a collection that stores items in sorted order


# Java Coding Patterns Cheat Sheet

---

# Two Pointers Pattern

## Use case
It is based on using two pointers (`left` and `right`) to traverse an array or string from both ends or in a single pass to reduce complexity from `O(n²)` to `O(n)`.

---

## All use cases
- Reverse array / string
- Palindrome check
- Remove duplicates (sorted array)
- Find pair with target sum (sorted array)

---

## Reverse Example
```text
[1,2,3,4] → [4,3,2,1]
``` 
``` java
int left = 0;
int right = arr.length - 1;

while(left < right) {
    int temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;

    left++;
    right--;
}
```

## Two sum example:
``` java
[1,2,3,4]
target = 7
→ [3,4]

HashMap<Integer, Integer> map = new HashMap<>();

for(int i = 0; i < nums.length; i++) {

    int diff = target - nums[i];

    if(map.containsKey(diff)) {
        System.out.println(diff + " " + nums[i]);
    }

    map.put(nums[i], i);
}
```

## Remove Duplicates Example
``` text
Uses:
slow pointer
fast pointer
[1,1,2,2,3]
→ [1,2,3]
```

``` java
int slow = 0;

for(int fast = 1; fast < nums.length; fast++) {

    if(nums[fast] != nums[slow]) {
        slow++;
        nums[slow] = nums[fast];
    }
}

```


sliding window string to find the larget unique substring
``` java
String s = "abcabcbb";

Set<Character> set = new HashSet<>();

int left = 0;
int max = 0;

for(int right = 0; right < s.length(); right++) {

    while(set.contains(s.charAt(right))) {

        set.remove(s.charAt(left));
        left++;
    }

    set.add(s.charAt(right));

    max = Math.max(max, right - left + 1);
}

System.out.println(max);
```

# Stack Pattern
## Use case
Stack pattern is used for problems that require LIFO (Last-In, First-Out) behavior or nested structure validation.

## Common Use Cases
1. **Parentheses Validation**: Checking balanced parentheses `()`, `{}`, `[]`.
2. **Expression Evaluation**: Evaluating postfix expressions or infix to postfix conversion.
3. **Next Greater Element**: Finding the next greater element for each element in an array.
4. **Monotonic Stack**: Problems involving increasing or decreasing subsequences.
5. **Backtracking**: DFS traversal where you need to backtrack (e.g., permutations, combinations).
6. **Window Problems**: Sliding window maximum/minimum using a monotonic stack.

## All Use Cases
- Valid Parentheses → `( { [ ] } )`
- Next Greater Element
- Trapping Rain Water
- Largest Rectangle in Histogram
- Parentheses Combinations
- Backtracking Problems
- Undo/Redo Operations
- Browser History Navigation

---

# Valid Parentheses Example

## Problem
Given a string containing just the characters `( ) { } [ ]`, determine if the input string is valid.

### Example 1:
```text
Input: "()"
Output: true
```

### Example 2:
```text
Input: "(]"
Output: false
```

### Example 3:
```text
Input: "()[]{}"
Output: true
```

## Solution
```java
public boolean isValid(String s) {

    Stack<Character> stack = new Stack<>();

    for(int i = 0; i < s.length(); i++) {

        char c = s.charAt(i);

        if(c == '(' || c == '{' || c == '[') {
            stack.push(c);
        } else {

            if(stack.isEmpty()) {
                return false;
            }

            char top = stack.pop();

            if((c == ')' && top != '(') ||
               (c == '}' && top != '{') ||
               (c == ']' && top != '[')) {
                return false;
            }
        }
    }

    return stack.isEmpty();
}
```

---

# Next Greater Element Example

## Problem
Find the next greater element for each element in an array.

### Example:
```text
Input:  [4, 5, 2, 25]
Output: [5, 25, 25, -1]
```

### Explanation:
- For 4, next greater is 5
- For 5, next greater is 25
- For 2, next greater is 25
- For 25, no greater element → -1

## Solution
```java
public int[] nextGreaterElement(int[] nums) {

    Stack<Integer> stack = new Stack<>();
    int[] result = new int[nums.length];

    for(int i = 0; i < nums.length; i++) {

        while(!stack.isEmpty() && nums[stack.peek()] < nums[i]) {
            result[stack.pop()] = nums[i];
        }

        stack.push(i);
    }

    while(!stack.isEmpty()) {
        result[stack.pop()] = -1;
    }

    return result;
}
```

---

# Monotonic Stack (Increasing) Example

## Problem
Find the previous smaller element for each element in an array.

### Example:
```text
Input:  [4, 5, 2, 10, 8]
Output: [-1, 4, -1, 2, 2]
```

### Explanation:
- For 4 → -1
- For 5 → 4
- For 2 → -1
- For 10 → 2
- For 8 → 2

## 💡 Solution
```java
public int[] previousSmaller(int[] nums) {

    Stack<Integer> stack = new Stack<>();
    int[] result = new int[nums.length];

    for(int i = 0; i < nums.length; i++) {

        while(!stack.isEmpty() && stack.peek() >= nums[i]) {
            stack.pop();
        }

        result[i] = stack.isEmpty() ? -1 : stack.peek();

        stack.push(nums[i]);
    }

    return result;
}
```

---

# 💡 Monotonic Stack (Decreasing) Example

## 🎯 Problem
Find the next greater element for each element in an array.

### Example:
```text
Input:  [4, 5, 2, 10, 8]
Output: [5, 10, 10, -1, -1]
```

### Explanation:
- For 4 → 5
- For 5 → 10
- For 2 → 10
- For 10 → -1
- For 8 → -1

## 💡 Solution
```java
public int[] nextGreater(int[] nums) {

    Stack<Integer> stack = new Stack<>();
    int[] result = new int[nums.length];

    for(int i = nums.length - 1; i >= 0; i--) {

        while(!stack.isEmpty() && stack.peek() <= nums[i]) {
            stack.pop();
        }

        result[i] = stack.isEmpty() ? -1 : stack.peek();

        stack.push(nums[i]);
    }

    return result;
}
```

---

# 🎯 Quick Tips for Stack Pattern

1. **Stack is LIFO**: Use it when you need to reverse something or process nested structures.
2. **Monotonic Stack**: If you need increasing/decreasing order, use a monotonic stack.
3. **Check Empty**: Always check `stack.isEmpty()` before `pop()` or `peek()`.
4. **Comparison**: When comparing, check both values and indices (sometimes you need the index for result array).
5. **Two-Pass**: Monotonic stack problems often require two passes (forward and backward) or clever logic to handle remaining elements.
6. **Space Complexity**: Stacks can use `O(n)` space in worst-case (e.g., sorted array).



# Merge Intervals

## Use Case
Merge overlapping intervals to produce a list of mutually exclusive intervals.

## Examples

### Example 1
```text
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
``` 

```java
import java.util.Arrays;
import java.util.LinkedList;
import java.util.List;

public class Solution {
    public int[][] merge(int[][] intervals) {

        // Sort by start time
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        LinkedList<int[]> merged = new LinkedList<>();

        for (int[] interval : intervals) {

            // No overlap → add new
            if (merged.isEmpty() || merged.getLast()[1] < interval[0]) {
                merged.add(interval);
            }
            // Overlap → merge
            else {
                merged.getLast()[1] = Math.max(merged.getLast()[1], interval[1]);
            }
        }

        return merged.toArray(new int[merged.size()][]);
    }
}
```

### Example 2
```text
Input: [[1,4],[4,5]]
Output: [[1,5]]
```

### Example 3
```text
Input: [[1,4],[2,3]]
Output: [[1,4]]
```

## Complexity
- Time: `O(n log n)` (due to sorting)
- Space: `O(n)` (or `O(log n)` depending on sort space)

## Key Insight
Sort by start time first → then merge in one pass.


#  Binary Search Pattern

## Use Case
Searching for an element in a **sorted** array efficiently.

## Key Idea
- Works only on sorted data
- Reduces search space by half each time
- O(log n) time complexity

## Basic Algorithm
```java
int binarySearch(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }

    return -1; // Not found
}
```

## Common Variations

### 1. Find First Occurrence
```java
// Find smallest index where nums[i] == target
while (left < right) {
    int mid = left + (right - left) / 2;

    if (nums[mid] < target) left = mid + 1;
    else right = mid; // Keep mid as possible answer
}

// After loop: if nums[left] == target, it's the first
```

### 2. Find Last Occurrence
```java
// Find largest index where nums[i] == target
while (left < right) {
    int mid = left + (right - left + 1) / 2; // Ceiling mid

    if (nums[mid] > target) right = mid - 1;
    else left = mid; // Keep mid as possible answer
}

// After loop: if nums[left] == target, it's the last
```

### 3. Search Rotated Sorted Array
```java
// Array is sorted but rotated (e.g., [4,5,6,7,0,1,2])

if (nums[mid] <= nums[right]) { // Right side sorted
    if (target >= nums[mid] && target <= nums[right]) {
        left = mid + 1;
    } else {
        right = mid - 1;
    }
} else { // Left side sorted
    if (target >= nums[left] && target <= nums[mid]) {
        right = mid - 1;
    } else {
        left = mid + 1;
    }
}
```

### 4. Find Element in Infinite Array
```java
// Array size unknown, can access any index

// 1. Find range where element might exist
int left = 0, right = 1;
while (nums[right] < target) {
    left = right;
    right *= 2;
}

// 2. Binary search in this range
return binarySearch(nums, target, left, right);
```

## When to Use
- Array is **sorted**
- Need O(log n) search time
- Problem asks for first/last occurrence
- Searching in rotated sorted array
- Finding elements in infinite arrays
