Is a form of DFS for graphs with no cycles and no undirected edges

## Example
```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (numCourses <= 0) return true;
        // Initialise inDegree array and adjacency list
        ArrayList<ArrayList<Integer>> adjList = new ArrayList<>();
        for(int i = 0; i < numCourses; i++){
            adjList.add(new ArrayList<Integer>());
        }
        // Build graph and update inDegree for each node
        int[] inDegree = new int[numCourses];
        for(int[] prereq : prerequisites){
            adjList.get(prereq[1]).add(prereq[0]);  
            inDegree[prereq[0]]++;
        }
        // Initialise the queue with courses having no prerequisites
        Deque<Integer> sources = new ArrayDeque<>();
        for (int i = 0; i < numCourses; i++){
            if(inDegree[i] == 0) sources.add(i);
        }

        int counter = 0;
        // Process nodes with no prerequisites
        while(!sources.isEmpty()){
            int course = sources.removeFirst();
            counter++;
            for(int child : adjList.get(course)){
                inDegree[child]--;
                if(inDegree[child] == 0) sources.add(child);
            }
        }
        System.out.println(counter);
        return counter == numCourses;
    }
}

```
