```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Edge>[] edges;
    private static boolean[] visited;
    private static int N, start, end;

    public static void main(String[] args) throws IOException {
        init();

        int answer = BFS();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        start = Integer.parseInt(st.nextToken());
        end = Integer.parseInt(st.nextToken());

        edges = new List[N+1];
        visited = new boolean[N+1];

        for (int i = 1; i <= N; i++) {
            edges[i] = new ArrayList<>();
        }

        for (int i = 1; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int node1 = Integer.parseInt(st.nextToken());
            int node2 = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            edges[node1].add(new Edge(node2, cost));
            edges[node2].add(new Edge(node1, cost));
        }
    }

    private static int BFS() {
        Queue<int[]> q = new ArrayDeque<>();
        visited[start] = true;
        int result = 0;
        // node, cost, max
        q.add(new int[]{start, 0, 0});

        while (!q.isEmpty()) {
            int[] current = q.poll();

            if (current[0] == end) {
                result = current[1]-current[2];
                break;
            }

            for (Edge edge : edges[current[0]]) {
                if (visited[edge.dest]) continue;
                visited[edge.dest] = true;
                int cost = current[1] + edge.cost;
                int max = Math.max(current[2], edge.cost);
                q.add(new int[]{edge.dest, cost, max});
            }
        }

        return result;
    }

    static class Edge {
        int dest;
        int cost;

        public Edge(int dest, int cost) {
            this.dest = dest;
            this.cost = cost;
        }
    }
}
```
