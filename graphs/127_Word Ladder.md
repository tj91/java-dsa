Approach
- Transform words to possible keys
  - create adjacency list
- perform BFS

```java
        public int ladderLength(String beginWord, String endWord, List<String> wordList) {

        Map<String, ArrayList<String>> adj = new HashMap<>();
        for (String word : wordList) { // N

            int l = word.length();

            for (int i = 0; i < l; i++) { // M

                String key = word.substring(0, i) + "." + word.substring(i + 1, l);
                // This above operations costs M
                ArrayList<String> edges = adj.getOrDefault(key, new ArrayList<>());
                edges.add(word);
                adj.put(key, edges);
            }

        }
        // ADJ is formed in O(N . M^2)
        Queue<String> que = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        visited.add(beginWord);
        que.add(beginWord);
        int d = 1;
        while (!que.isEmpty()) {
            int size = que.size();
            d++;
            for (int j = 0; j < size; j++) {

                String word = que.poll();
                int l = word.length();
                for (int i = 0; i < l; i++) {

                    String key = word.substring(0, i) + "." + word.substring(i + 1, l);
                    for (String neighbor : adj.getOrDefault(key, new ArrayList<>())) {
                        if (!visited.contains(neighbor)) {
                            if (neighbor.equals(endWord)) {
                                return d;
                            }
                            que.add(neighbor);
                            visited.add(neighbor);
                        }

                    }

                }
            }
        }

        return 0;

    }
```
