- used for searching pairs in a sorted array

As the name suggests, we use two pointers `low` and `high` but the key is we perform a single iteration of the array. We mark `low` as 0 (beginning of the array) and `high` as size-1 (end of the array).

We calculate `arr[low]+arr[high]` and check:
1. If `arr[low]+arr[high] < sum`, we increment the `low` pointer.
2. If `arr[low]+arr[high] = sum`, we print `low` and `high`
3. If `arr[low]+arr[high] > sum`, we decrement the `high` pointer.
## Example
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);

        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i-1]) {
                continue;
            }
            
            int j = i + 1;
            int k = nums.length - 1;

            while (j < k) {
                int total = nums[i] + nums[j] + nums[k];

                if (total > 0) {
                    k--;
                } else if (total < 0) {
                    j++;
                } else {
                    res.add(Arrays.asList(nums[i], nums[j], nums[k]));
                    j++;

                    while (nums[j] == nums[j-1] && j < k) {
                        j++;
                    }
                }
            }
        }
        return res;        
    }
}

```