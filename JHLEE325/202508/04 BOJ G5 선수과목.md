```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        StringBuilder sb = new StringBuilder();

        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        List<List<Integer>> graph = new ArrayList<>(n + 1);
        for (int i = 0; i <= n; i++) graph.add(new ArrayList<>());

        int[] indeg = new int[n + 1];
        int[] semester = new int[n + 1];

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            graph.get(a).add(b);
            indeg[b]++;
        }

        Deque<Integer> q = new ArrayDeque<>();
        for (int i = 1; i <= n; i++) {
            if (indeg[i] == 0) {
                semester[i] = 1;
                q.offer(i);
            }
        }

        while (!q.isEmpty()) {
            int cur = q.poll();
            for (int nxt : graph.get(cur)) {
                semester[nxt] = Math.max(semester[nxt], semester[cur] + 1);
                if (--indeg[nxt] == 0) q.offer(nxt);
            }
        }

        for (int i = 1; i <= n; i++) {
            sb.append(semester[i]).append(' ');
        }
        System.out.println(sb.toString().trim());
    }
}

```
