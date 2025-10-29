```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine().trim());
        StringBuilder sb = new StringBuilder();

        for (int t = 0; t < T; t++) {
            int n = Integer.parseInt(br.readLine().trim());

            st = new StringTokenizer(br.readLine());
            int[] lastYear = new int[n];
            for (int i = 0; i < n; i++) {
                lastYear[i] = Integer.parseInt(st.nextToken());
            }

            boolean[][] graph = new boolean[n + 1][n + 1];
            int[] indegree = new int[n + 1];

            for (int i = 0; i < n; i++) {
                for (int j = i + 1; j < n; j++) {
                    int higher = lastYear[i];
                    int lower = lastYear[j];
                    if (!graph[higher][lower]) {
                        graph[higher][lower] = true;
                        indegree[lower]++;
                    }
                }
            }

            int m = Integer.parseInt(br.readLine().trim());
            for (int i = 0; i < m; i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());

                if (graph[a][b]) {
                    graph[a][b] = false;
                    indegree[b]--;
                    graph[b][a] = true;
                    indegree[a]++;
                } else if (graph[b][a]) {
                    graph[b][a] = false;
                    indegree[a]--;
                    graph[a][b] = true;
                    indegree[b]++;
                } else {
                    graph[a][b] = true;
                    indegree[b]++;
                }
            }

            Queue<Integer> q = new LinkedList<>();
            for (int i = 1; i <= n; i++) {
                if (indegree[i] == 0) {
                    q.offer(i);
                }
            }

            boolean ispossible = false;
            List<Integer> result = new ArrayList<>();

            for (int cnt = 0; cnt < n; cnt++) {
                if (q.isEmpty()) {
                    result = null;
                    break;
                }
                if (q.size() > 1) {
                    ispossible = true;
                }
                int cur = q.poll();
                result.add(cur);

                for (int next = 1; next <= n; next++) {
                    if (graph[cur][next]) {
                        indegree[next]--;
                        if (indegree[next] == 0) {
                            q.offer(next);
                        }
                    }
                }
            }

            if (result == null) {
                sb.append("IMPOSSIBLE\n");
            } else if (ispossible) {
                sb.append("?\n");
            } else {
                for (int x : result) {
                    sb.append(x).append(" ");
                }
                sb.append("\n");
            }
        }

        System.out.print(sb.toString());
    }
}
```
