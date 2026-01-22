```java
import java.io.*;
import java.util.*;

public class BJ_5719_거의_최단_경로 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int N, M, S, D, shortest;
    private static int[] dist, distFor, distBack;
    private static List<Node>[] graphFor, graphBack;
    private static Queue<Node> pq;

    private static class Node implements Comparable<Node> {
        int to;
        int cost;

        public Node(int to, int cost) {
            this.to = to;
            this.cost = cost;
        }

        @Override
        public int compareTo(Node o) {
            return Integer.compare(this.cost, o.cost);
        }

    }

    public static void main(String[] args) throws IOException {
        while (init()) {
            sol();
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

    private static boolean init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        if (N == 0 && M == 0) return false;

        st = new StringTokenizer(br.readLine());
        S = Integer.parseInt(st.nextToken());
        D = Integer.parseInt(st.nextToken());

        graphFor = new List[N];
        graphBack = new List[N];
        for (int i = 0; i < N; i++) {
            graphFor[i] = new ArrayList<>();
            graphBack[i] = new ArrayList<>();
        }

        dist = new int[N];
        distFor = new int[N];
        distBack = new int[N];
        Arrays.fill(dist, 987654321);
        Arrays.fill(distFor, 987654321);
        Arrays.fill(distBack, 987654321);

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            graphFor[a].add(new Node(b, c));
            graphBack[b].add(new Node(a, c));
        }

        pq = new PriorityQueue<>();
        return true;
    }

    private static void sol() {
        dijkstra(S, D, distFor, graphFor);
        dijkstra(D, S, distBack, graphBack);
        shortest = distFor[D];

        findRoute();
    }

    private static void dijkstra(int start, int end, int[] dist, List<Node>[] graph) {
        pq.clear();
        pq.add(new Node(start, 0));
        dist[start] = 0;

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (dist[cur.to] < cur.cost) continue;

            if (cur.to == end) break;

            for (Node next : graph[cur.to]) {
                int nextCost = dist[cur.to] + next.cost;

                if (nextCost < dist[next.to]) {
                    dist[next.to] = nextCost;
                    pq.add(new Node(next.to, nextCost));
                }
            }
        }
    }

    private static void findRoute() {
        pq.clear();
        pq.offer(new Node(S, 0));
        dist[S] = 0;

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (dist[cur.to] < cur.cost) continue;

            if (cur.to == D) {
                sb.append(dist[cur.to]).append("\n");
                return;
            }

            for (Node next : graphFor[cur.to]) {
                if (distFor[cur.to] + next.cost + distBack[next.to] == shortest) continue;

                int nextCost = dist[cur.to] + next.cost;

                if (nextCost < dist[next.to]) {
                    dist[next.to] = nextCost;
                    pq.offer(new Node(next.to, nextCost));
                }
            }
        }
        sb.append("-1\n");
    }

}
```
