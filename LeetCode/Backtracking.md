- time complexity - $O(2^n)$ 
## Example
```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, 0);
    return list;
}

private void backtrack(List<List<Integer>> list , List<Integer> tempList, int [] nums, int start){
    list.add(new ArrayList<>(tempList));
	// the iterative process
    for(int i = start; i < nums.length; i++){
		// go down the route
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
		// the backtrack
        tempList.remove(tempList.size() - 1);
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