Traverse a graph in distance from root node (closest are seen first)
- Create an empty queue and a list of visited
- add root node to queue
- visit all queue members, popping them from the queue, adding them to the list of visited and pushing their unvisited children to the queue
- repeat till queue is empty
## Example
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue= new LinkedList<TreeNode>();
        List<List<Integer>> ans= new ArrayList<>();
        if(root == null) return ans;
        queue.offer(root);  // add root in queue
        while(!queue.isEmpty()){
            int currLevel= queue.size();
            List<Integer> temp= new ArrayList<>();
            for(int i=0; i< currLevel; i++){
                if(queue.peek().left != null) queue.offer(queue.peek().left);  // if curr has any left than add in queue
                if(queue.peek().right != null) queue.offer(queue.peek().right); // if curr has any right than add in queue
                temp.add(queue.poll().val);  // poll will add the curr val in queue and will remove from queue as well
            }
            ans.add(temp);
        }
        return ans;
    }

    // offer - add in queue
    // peek - will return the element and keep it in queue
    // poll - will return the elelement and remove it from the queue
}

```