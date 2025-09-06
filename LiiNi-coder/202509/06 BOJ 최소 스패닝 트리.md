```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main {
    private static BufferedReader br;
    private static int V, E;
    private static ArrayList<Edge>[] adj;
    private static boolean[] visited;
    private static class Edge implements Comparable<Edge> {
        int to, weight;
        public Edge(int to, int weight) {
            this.to = to;
            this.weight = weight;
        }
        @Override
        public int compareTo(Edge other) {
            return this.weight - other.weight;
        }
    }

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());
        adj = new ArrayList[V + 1];
        for (int i = 1; i <= V; i++) {
            adj[i] = new ArrayList<>();
        }

        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());

            adj[u].add(new Edge(v, w));
            adj[v].add(new Edge(u, w));
        }

        System.out.println(prim());
    }

    private static long prim() {
        boolean[] visited = new boolean[V + 1];
        PriorityQueue<Edge> pq = new PriorityQueue<>();
        long totalWeight = 0;
        int visitedCount = 0;

        visited[1] = true;
        visitedCount++;
        for (Edge e : adj[1]) {
            pq.add(e);
        }

        while (!pq.isEmpty()) {
            Edge edge = pq.poll();
            if (visited[edge.to]) continue;
            visited[edge.to] = true;
            totalWeight += edge.weight;
            visitedCount++;
            for (Edge e : adj[edge.to]) {
                if (!visited[e.to]) {
                    pq.add(e);
                }
            }
            if (visitedCount == V) break;
        }

        return totalWeight;
    }
}

```
