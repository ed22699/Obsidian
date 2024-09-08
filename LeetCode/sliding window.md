Used for finding subarrays in O(n) time
- you have a `left` and a `right` pointer along with a `maxSubarray` value
- loop through the array, if condition is false you move the left pointer
## Example
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> visited = new HashMap<Character, Integer>();
        int n = s.length();
        int max = 0;
        int left = 0;
        for(int right = 0; right < n; right++){
            char letter = s.charAt(right);
            if(visited.get(letter) != null && visited.get(letter) >= left){
                left = visited.get(letter) + 1;
            }
            visited.put(letter, right);
            max = Math.max(right-left + 1, max);
        }
        return max;
    }
}
```