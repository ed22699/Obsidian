- time complexity - $O(2^n)$ 
## Example
```java
class Solution {
	public List<List<Integer>> subsets(int[] nums) {
		// create result list
		List<List<Integer>> res = new ArrayList<>();
		// create the subsets
		List<Integer> subsets = new ArrayList<>();
		// call recursive algorithm
		create_subset(0, nums, subsets, res);
		return res;
	}
	
	private void create_subset(int i, int[] nums, List<Integer> subset, List<List<Integer>> res){
		// if at length add subset to res and stopping condition
		if (i == nums.length){
			res.add(new ArrayList<>(subset));
			return;
		}
		// add element and recurse
		subset.add(nums[i]);
		create_subset(i+1, nums, subset, res);
		// backtrack
		subset.remove(subset.size() - 1);
		create_subset(i+1, nums, subset, res);
		}
}
```
First of all, we have two choices for `1`. We can create two subsets.
```csharp
[1] or []
```
Next, we have two choices for `2`. We need to think about each pattern (= `[1] or []`).
For `[1]` case, we can create subsets
```csharp
[1,2] or [1]

[1,2] is including 2 
[1] is not including 2 
```
For `[]` case, we can create subsets
```csharp
[2] or []

[2] is including 2 
[] is not including 2 
```
We have 4 subsets so far.
```csharp
[1,2], [1], [2], []
```