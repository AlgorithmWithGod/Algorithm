```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Integer>[] graph;
    private static int[] visited;
    private static int V, E;

    public static void main(String[] args) throws IOException {
        int K = Integer.parseInt(br.readLine());

        while (K-- > 0) {
            init();

            boolean result = true;

            for (int i = 1; i <= V; i++) {
                if (visited[i] == 0) {
                    result = BFS(i);
                }

                if (!result) break;
            }

            if (result) bw.write("YES" + "\n");
            else bw.write("NO" + "\n");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());

        visited = new int[V + 1];
        graph = new List[V + 1];

        for (int i = 0; i <= V; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            graph[a].add(b);
            graph[b].add(a);
        }
    }

    private static boolean BFS(int start) {
        Queue<Integer> q = new ArrayDeque<>();
        visited[start] = 1;
        q.add(start);

        while (!q.isEmpty()) {
            int current = q.poll();

            for (int next : graph[current]) {
                if (visited[next] == visited[current]) return false;

                if (visited[next] == 0) {
                    visited[next] = 3 - visited[current];
                    q.add(next);
                }
            }
        }

        return true;
    }
}
```
