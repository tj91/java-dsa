

Approach
- Traverse the tree using Preorder (DFS)
  - maintain a TreeMap tracking each column
  - for each column we have List<int[]> which maintains the row and the value
  - we sort by row and value for the final result

```java
 public List<List<Integer>> verticalTraversal(TreeNode root) {

        TreeMap<Integer, List<int[]>> map = new TreeMap<>();
        verticalTraversalHelper(map, root, 0, 0);

        List<List<Integer>> result = new ArrayList<>();

        for (List<int[]> row : map.values()) {

            row.sort((a, b) -> {
                if (a[0] == b[0]) { // for same row
                    return a[1] - b[1];
                }
                return a[0] - b[0];
            });
            List<Integer> resRow = new ArrayList<>();
            for (int[] r : row) {
                resRow.add(r[1]);
            }
            result.add(resRow);
        }
        return result;
    }

    void verticalTraversalHelper(TreeMap<Integer, List<int[]>> map, TreeNode root, int x, int y) {

        if (root == null) {
            return;
        }

        int[] a = { y, root.val }; // row , val
        if (map.containsKey(x)) {
            map.get(x).add(a);
        } else {
            List<int[]> list = new ArrayList<>();
            list.add(a);
            map.put(x, list);
        }
        verticalTraversalHelper(map, root.left, x - 1, y + 1);
        verticalTraversalHelper(map, root.right, x + 1, y + 1);
    }
```





