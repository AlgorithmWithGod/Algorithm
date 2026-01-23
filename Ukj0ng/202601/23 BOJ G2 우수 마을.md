```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Integer>[] graph;
    private static int[][] dp;
    private static int[] nodes;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();
        DFS(1, -1);

        bw.write(Math.max(dp[1][0], dp[1][1]) + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());

        graph = new List[N+1];
        dp = new int[N+1][2];
        nodes = new int[N+1];

        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
            nodes[i] = Integer.parseInt(st.nextToken());
        }

        for (int i = 0; i < N-1; i++) {
            st = new StringTokenizer(br.readLine());
            int U = Integer.parseInt(st.nextToken());
            int V = Integer.parseInt(st.nextToken());

            graph[U].add(V);
            graph[V].add(U);
        }
    }

    private static void DFS(int current, int parent) {
        dp[current][0] = nodes[current];
        dp[current][1] = 0;
        for (int next : graph[current]) {
            if (next == parent) continue;
            DFS(next, current);

            dp[current][0] += dp[next][1];
            dp[current][1] += Math.max(dp[next][0], dp[next][1]);
        }
    }
}
```
