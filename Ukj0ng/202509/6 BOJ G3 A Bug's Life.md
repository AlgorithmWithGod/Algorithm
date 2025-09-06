```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Integer>[] graph;
    private static int[] visited;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());

        for (int i = 1; i <= T; i++) {
            init();
            boolean result = true;

            for (int ii = 1; ii <= N; ii++) {
                if (visited[ii] == 0) {
                    result = BFS(ii);
                }

                if (!result) break;
            }

            bw.write(String.format("Scenario #%d:\n", i));
            if (result) bw.write("No suspicious bugs found!\n\n");
            else bw.write("Suspicious bugs found!\n\n");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        graph = new List[N+1];
        visited = new int[N+1];

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
    }

    private static boolean BFS(int start) {
        Queue<Integer> q = new ArrayDeque<>();
        visited[start] = 1;
        q.add(start);

        while (!q.isEmpty()) {
            int current = q.poll();

            for (int next : graph[current]) {
                if (visited[next] == 0) {
                    visited[next] = 3 - visited[current];
                    q.add(next);
                } else if (visited[next] == visited[current]) return false;
            }
        }

        return true;
    }
}
```
