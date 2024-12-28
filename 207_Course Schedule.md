- Detect cycle in a graph
  - Use DFS

```
    public boolean canFinish(int numCourses, int[][] prerequisites) {

        int n = numCourses;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            adj.add(new ArrayList<>());
        }

        // create graph
        for (int[] dep : prerequisites) {
            adj.get(dep[1]).add(dep[0]);
        }

        boolean[] visited = new boolean[n];
        boolean[] recStack = new boolean[n];
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                if (dfs(adj, i, visited, recStack)) {
                    return false;
                }
            }
        }
        return true;
    }

    boolean dfs(ArrayList<ArrayList<Integer>> adj, int i, boolean[] visited, boolean[] recStack) {

        if (recStack[i]) {
            return true;
        }

        if (visited[i]) {
            return false;
        }

        visited[i] = true;
        recStack[i] = true;

        for (int neighbor : adj.get(i)) {

            if (dfs(adj, neighbor, visited, recStack)) {
                return true;
            }
        }

        recStack[i] = false;
        return false;
    }
```
