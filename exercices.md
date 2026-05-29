# Two sum:

``` java
public static int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> indexs = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (indexs.containsKey(complement)) {
                return new int[] { indexs.get(complement), i };
            }
            indexs.put(nums[i], i);
        }

        return new int[] {};
    }

    public static void main(String[] args) {
        int[] nums = {2,7,11,15};
        int target = 9;

        int[] result = twoSum(nums, target);
        System.out.println(Arrays.toString(result));
    }

```

# Reverse string
``` java
 public static void main(String[] args) {
       String name = "hello";
       char [] arr = name.toCharArray();
       int left =0;
       int right = arr.length -1;
       
       for (int i = 0; i < arr.length; i++){
         while(left < right){
             char tmp = arr[left];
            arr[left] = arr[right];
            arr[right] = tmp;
            left++;
            right--;
         }
       
       }
       System.out.print(new String(arr));
    }
```

# Valid Parentheses
``` java
 import java.util.*;

public class Solution {

    public static void main(String[] args) { // Main method: program starts here
        String printhises = "{[()]}"; // Input string of brackets
        char[] arr = printhises.toCharArray(); // Convert string to character array
        Stack<Character> stack = new Stack<>(); // Stack to store opening brackets

        for (int i = 0; i < arr.length; i++) { // Loop through each character in the array
            if (arr[i] == '(' || arr[i] == '{' || arr[i] == '[') { // If character is an opening bracket
                stack.push(arr[i]); // Put it into the stack
            } else { // If character is a closing bracket
                if (stack.isEmpty()) { // If nothing is in the stack, it is invalid
                    System.out.println(false);
                    return;
                }

                char top = stack.pop(); // Remove the last opening bracket from the stack

                if ((arr[i] == ')' && top != '(') || // Check if ) matches (
                    (arr[i] == '}' && top != '{') || // Check if } matches {
                    (arr[i] == ']' && top != '[')) { // Check if ] matches [
                    System.out.println(false); // Not valid
                    return; // Stop program
                }
            }
        }

        if (stack.isEmpty()) { // If stack is empty, all brackets matched
            System.out.println(true); // Valid
        } else { // If stack still has items, brackets did not match
            System.out.println(false); // Invalid
        }
    }
}
```
```text
input: () [] {} 
output: true

input: (] -> false
```

# Anagram like "listen" and "silent"
``` java
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        String s1 = "listen";
        String s2 = "silent";
        System.out.println(isAnagram(s1, s2)); // Output: true
    }

    public static boolean isAnagram(String s1, String s2) {
        // If lengths are different, they cannot be anagrams
        if (s1.length() != s2.length()) {
            return false;
        }

        // Convert strings to char arrays
        char[] arr1 = s1.toCharArray();
        char[] arr2 = s2.toCharArray();

        // Sort the char arrays
        Arrays.sort(arr1);
        Arrays.sort(arr2);

        // Compare the sorted arrays
        return Arrays.equals(arr1, arr2);
    }
}

```
# # find longest subString 
```java
int left = 0;
int right =0;
int max = 0;
HashSet<Character> set = new HashSet<>();
String s = "abcabcbb";

while(right < s.length()){
    if(!set.contains(s.charAt(right))){
        set.add(s.charAt(right));
        right ++;
        max = Math.max(max, set.size());
    }else{
        set.remove(s.charAt(left));
        left ++;
    }
}

```
