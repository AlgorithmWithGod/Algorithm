```java
import java.io.*;
import java.util.*;

public class Main {

    static List<Integer>[] graph;
    static boolean[] visited;
    static boolean isgraph;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        int T = Integer.parseInt(br.readLine());

        for (int t=0;t<T;t++) {
            StringTokenizer st;
            int N = Integer.parseInt(br.readLine());
            int M = Integer.parseInt(br.readLine());

            graph = new ArrayList[N + 1];
            visited = new boolean[N + 1];
            isgraph = false;

            for (int i = 1; i <= N; i++) {
                graph[i] = new ArrayList<>();
            }

            for (int i = 0; i < M; i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());

                graph[a].add(b);
                graph[b].add(a);
            }

            if (M != N - 1) {
                sb.append("graph\n");
                continue;
            }

            dfs(1, -1);

            boolean connected = true;
            for (int i = 1; i <= N; i++) {
                if (!visited[i]) {
                    connected = false;
                    break;
                }
            }

            if (isgraph || !connected) {
                sb.append("graph\n");
            } else {
                sb.append("tree\n");
            }
        }

        System.out.print(sb);
    }

    static void dfs(int cur, int parent) {
        visited[cur] = true;

        for (int next : graph[cur]) {
            if (!visited[next]) {
                dfs(next, cur);
            } else if (next != parent) {
                isgraph = true;
            }
        }
    }
}
```
