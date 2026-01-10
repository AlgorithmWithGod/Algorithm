```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = (int) 2e9 + 10;
    private static List<Edge>[] edges;
    private static int[][] dist;
    private static int V, E;

    public static void main(String[] args) throws IOException {
        init();
        dijkstra(1);

        for (int i = 2; i <= V; i++) {
            bw.write(Math.min(dist[i][0], dist[i][1]) + "\n");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());

        edges = new List[V+1];
        dist = new int[V+1][2];

        for (int i = 1; i <= V; i++) {
            edges[i] = new ArrayList<>();
        }

        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());
            int node1 = Integer.parseInt(st.nextToken());
            int node2 = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            int taste = Integer.parseInt(st.nextToken());

            edges[node1].add(new Edge(node2, cost, taste));
            edges[node2].add(new Edge(node1, cost, taste));
        }
    }

    private static void dijkstra(int start) {
        PriorityQueue<Edge> pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o1.cost, o2.cost));
        for (int i = 1; i <= V; i++) {
            dist[i][0] = INF;
            dist[i][1] = INF;
        }
        dist[start][0] = 0;
        pq.add(new Edge(1, 0, false));

        while (!pq.isEmpty()) {
            Edge current = pq.poll();

            if (current.eat && current.cost > dist[current.dest][1]) continue;
            if (!current.eat && current.cost > dist[current.dest][0]) continue;

            for (Edge next : edges[current.dest]) {
                int nCost = current.cost + next.cost;
                if (!current.eat && nCost < dist[next.dest][0]) {
                    dist[next.dest][0] = nCost;
                    pq.add(new Edge(next.dest, nCost, false));
                }
                if (current.eat && nCost < dist[next.dest][1]) {
                    dist[next.dest][1] = nCost;
                    pq.add(new Edge(next.dest, nCost, true));
                }
                nCost -= next.taste;
                if (!current.eat && nCost < dist[next.dest][1]) {
                    dist[next.dest][1] = nCost;
                    pq.add(new Edge(next.dest, nCost, true));
                }
            }
        }
    }

    static class Edge {
        int dest;
        int cost;
        int taste;
        boolean eat;

        public Edge(int dest, int cost, int taste) {
            this.dest = dest;
            this.cost = cost;
            this.taste = taste;
            this.eat = false;
        }

        public Edge(int dest, int cost, boolean eat) {
            this.dest = dest;
            this.cost = cost;
            this.eat = eat;
        }
    }
}
```
