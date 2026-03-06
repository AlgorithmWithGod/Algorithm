```
import java.io.*;

import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.List;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Integer>[] graph;
    private static int[][] depth;
    private static boolean[] visited;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        graph = new List[N+1];
        depth = new int[N+1][2];
        visited = new boolean[N+1];

        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < N-1; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int node1 = Integer.parseInt(st.nextToken());
            int node2 = Integer.parseInt(st.nextToken());

            graph[node1].add(node2);
            graph[node2].add(node1);
        }

        BFS();

        M = Integer.parseInt(br.readLine());
        for (int i = 0; i < M; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int node1 = Integer.parseInt(st.nextToken());
            int node2 = Integer.parseInt(st.nextToken());

            int depth1 = depth[node1][0];
            int depth2 = depth[node2][0];

            while (depth1 != depth2) {
                if (depth1 > depth2) {
                    node1 = depth[node1][1];
                    depth1 = depth[node1][0];
                } else {
                    node2 = depth[node2][1];
                    depth2 = depth[node2][0];
                }
            }

            while (node1 != node2) {
                node1 = depth[node1][1];
                node2 = depth[node2][1];
            }

            bw.write(node1 + "\n");
        }
    }

    private static void BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        depth[1][0] = 1;
        depth[1][1] = -1;
        visited[1] = true;
        q.add(new int[] {1, 1});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            for (int next : graph[current[0]]) {
                if (visited[next]) continue;
                depth[next][0] = current[1]+1;
                depth[next][1] = current[0];
                visited[next] = true;
                q.add(new int[]{next, current[1]+1});
            }
        }
    }
}
```
