```java
import java.util.*;

class Solution {
    public int solution(int n, int[][] wires) {
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i <= n; i++) g.add(new ArrayList<>());

        for (int[] w : wires) {
            g.get(w[0]).add(w[1]);
            g.get(w[1]).add(w[0]);
        }

        int answer = Integer.MAX_VALUE;

        for (int[] cut : wires) {
            int a = cut[0];
            int b = cut[1];

            int sizeA = bfsCount(n, g, a, b);
            int sizeB = n - sizeA;
            int diff = Math.abs(sizeA - sizeB);

            if (diff < answer) answer = diff;
        }

        return answer;
    }

    private int bfsCount(int n, List<List<Integer>> g, int a, int b) {
        boolean[] visited = new boolean[n + 1];
        Queue<Integer> q = new LinkedList<>();
        q.add(a);
        visited[a] = true;

        int cnt = 0;

        while (!q.isEmpty()) {
            int cur = q.poll();
            cnt++;

            for (int nxt : g.get(cur)) {
                if (isCutEdge(cur, nxt, a, b)) continue;
                if (!visited[nxt]) {
                    visited[nxt] = true;
                    q.add(nxt);
                }
            }
        }
        return cnt;
    }

    private boolean isCutEdge(int u, int v, int a, int b) {
        return (u == a && v == b) || (u == b && v == a);
    }
}

```
