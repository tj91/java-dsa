Approach
 - Detect cycle in graph
   - DFS with topological sort


```java
  public int[] findOrder(int numCourses, int[][] prerequisites) {

        int n = numCourses;

        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            adj.add(new ArrayList<>());

        }

        for (int[] dep : prerequisites) {
            adj.get(dep[1]).add(dep[0]);
        }

        ArrayList<Integer> res = new ArrayList<Integer>();
        boolean[] visited = new boolean[n];
        boolean[] recStack = new boolean[n];
        boolean isCyclic = false;
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                isCyclic = dfs(adj, i, visited, recStack, res);

                if (isCyclic) {
                    return new int[0];
                }
            }
        }



        Collections.reverse(res);

        int[] resArr = new int[res.size()];
        for (int i = 0; i < res.size(); i++) {
            resArr[i] = res.get(i);
        }
        return resArr;
    }

    boolean dfs(ArrayList<ArrayList<Integer>> adj, int i, boolean[] visited, boolean[] recStack,
            ArrayList<Integer> res) {

        if (recStack[i]) {
            return true;
        }

        if (visited[i]) {
            return false;
        }

        recStack[i] = true;
        visited[i] = true;

        for (int neighbor : adj.get(i)) {

            if (dfs(adj, neighbor, visited, recStack, res)) {
                return true;
            }
        }

        res.add(i); // we add the vertex once done with all the neighbors
        recStack[i] = false;
        return false;
    }
```
