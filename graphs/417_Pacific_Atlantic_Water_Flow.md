
Approach
- Traverse the graph for Atlantic 
  - Use BFS
- Traverse the graph for Pacific
  - Use BFS
- Traverse both visited matrices to find cells from which water can flow to both Pac and Atl



```java

    public List<List<Integer>> pacificAtlantic(int[][] heights) {

        int r = heights.length;
        int c = heights[0].length;
        int[][] atl = new int[r][c];

        List<List<Integer>> res = new ArrayList<>();

        Queue<int[]> q = new LinkedList<>();
        for (int i = 0; i < r; i++) {
            atl[i][c - 1] = 1;
            int[] arr = { i, c - 1 };
            q.add(arr);
        }

        for (int j = 0; j < c; j++) {
            atl[r - 1][j] = 1;
            int[] arr = { r - 1, j };
            q.add(arr);
        }

        bfs(q, heights, atl);

        int[][] pac = new int[r][c];

        q = new LinkedList<>();
        for (int i = 0; i < r; i++) {
            pac[i][0] = 1;
            int[] arr = { i, 0 };
            q.add(arr);
        }

        for (int j = 0; j < c; j++) {
            pac[0][j] = 1;
            int[] arr = { 0, j };
            q.add(arr);
        }

        bfs(q, heights, pac);

        int count = 0;

        for (int i = 0; i < r; i++) {

            for (int j = 0; j < c; j++) {

                if (atl[i][j] == 1 && pac[i][j] == 1) {
                    ArrayList<Integer> list = new ArrayList<>();
                    list.add(i);list.add(j);
                    res.add(list);
                }
            }
        }

        return res;
    }

    void bfs(Queue<int[]> q, int[][] heights, int[][] arr) {


        int r = heights.length;
        int c = heights[0].length;
        int[][] directions = { { 1, 0 }, { -1, 0 }, { 0, 1 }, { 0, -1 } };

        while (!q.isEmpty()) {

            int[] cur = q.poll();
            for (int[] move : directions) {
                int posx = cur[0] + move[0];
                int posy = cur[1] + move[1];

                if (posx >= 0 && posx < r && posy >= 0 && posy < c && arr[posx][posy] == 0
                        && heights[posx][posy] >= heights[cur[0]][cur[1]]) {

                    arr[posx][posy] = 1;
                    int[] a = { posx, posy };
                    // 
                    q.add(a);
                }

            }

        }
    }

```
