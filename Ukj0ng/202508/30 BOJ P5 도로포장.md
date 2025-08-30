```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final long INF = (long) 5e10 + 10;
    private static List<Node>[] graph;
    private static long[][] dist;
    private static int N, M, K;

    public static void main(String[] args) throws IOException {
        init();
        dijkstra(1);
        long answer = INF;
        for (int i = 0; i <= K; i++) {
            answer = Math.min(answer, dist[N][i]);
        }
        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        graph = new List[N+1];
        dist = new long[N+1][K+1];

        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 1; i <= M; i++) {
            st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());

            graph[start].add(new Node(end, cost));
            graph[end].add(new Node(start, cost));
        }
    }

    private static void dijkstra(int start) {
        PriorityQueue<Node> pq = new PriorityQueue<>((o1, o2) -> Long.compare(o1.cost, o2.cost));
        for (int i = 1; i <= N; i++) {
            Arrays.fill(dist[i], INF);
        }
        dist[start][0] = 0;
        pq.add(new Node(start, dist[start][0], 0));

        while (!pq.isEmpty()) {
            Node current = pq.poll();

            if (current.cost > dist[current.dest][current.pavement]) continue;

            for (Node next : graph[current.dest]) {
                if (current.pavement+1 <= K && dist[current.dest][current.pavement]< dist[next.dest][current.pavement+1]) {
                    dist[next.dest][current.pavement+1] = dist[current.dest][current.pavement];
                    pq.add(new Node(next.dest, dist[next.dest][current.pavement+1], current.pavement+1));
                }

                if (dist[current.dest][current.pavement] + next.cost < dist[next.dest][current.pavement]) {
                    dist[next.dest][current.pavement] = dist[current.dest][current.pavement] + next.cost;
                    pq.add(new Node(next.dest, dist[next.dest][current.pavement], current.pavement));
                }
            }
        }
    }

    static class Node {
        int dest;
        long cost;
        int pavement;

        Node (int dest, long cost) {
            this.dest = dest;
            this.cost = cost;
            this.pavement = 0;
        }

        Node (int dest, long cost, int pavement) {
            this.dest = dest;
            this.cost = cost;
            this.pavement = pavement;
        }
    }
}
```
