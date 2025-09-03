```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final long INF = (long) 1e15 + 10;
    private static List<Edge>[] graph;
    private static long[][] dist;
    private static int N, M, K, S, T;

    public static void main(String[] args) throws IOException {
        init();
        dijkstra(S);

        long answer = -1;
        if (dist[T][0] != INF) {
            answer = dist[T][0];
        }

        if (answer == -1) bw.write("IMPOSSIBLE" + "\n");
        else bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        st = new StringTokenizer(br.readLine());
        S = Integer.parseInt(st.nextToken());
        T = Integer.parseInt(st.nextToken());

        graph = new List[N + 1];
        dist = new long[N + 1][K];

        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            long cost = Long.parseLong(st.nextToken());

            graph[a].add(new Edge(b, cost));
        }
    }

    private static void dijkstra(int start) {
        PriorityQueue<Edge> pq = new PriorityQueue<>((o1, o2) -> Long.compare(o1.cost, o2.cost));
        for (int i = 1; i <= N; i++) {
            Arrays.fill(dist[i], INF);
        }
        dist[start][0] = 0;
        pq.add(new Edge(start, 0, 0));

        while (!pq.isEmpty()) {
            Edge current = pq.poll();

            if (current.cost > dist[current.dest][current.state]) continue;

            for (Edge next : graph[current.dest]) {
                long nCost = current.cost + next.cost;
                int nState = (int) (nCost % K);

                if (nCost < dist[next.dest][nState]) {
                    dist[next.dest][nState] = nCost;
                    pq.add(new Edge(next.dest, dist[next.dest][nState], nState));
                }
            }
        }
    }

    static class Edge {
        int dest;
        long cost;
        int state;

        public Edge(int dest, long cost, int state) {
            this.dest = dest;
            this.cost = cost;
            this.state = state;
        }

        public Edge(int dest, long cost) {
            this.dest = dest;
            this.cost = cost;
            this.state = 0;
        }
    }
}
```
