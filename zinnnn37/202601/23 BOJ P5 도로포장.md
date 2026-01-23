```java
import java.io.*;
import java.util.*;

public class BJ_1162_도로포장 {

    private static final long INF = 50_000_000_001L;

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M, K;
    private static long[][]     dist;
    private static List<Node>[] graph;
    private static Queue<Node>  pq;

    private static class Node implements Comparable<Node> {
        int  to;
        long cost;
        int  cnt;

        public Node(int to, long cost, int cnt) {
            this.to = to;
            this.cost = cost;
            this.cnt = cnt;
        }

        @Override
        public int compareTo(Node o) {
            return Long.compare(this.cost, o.cost);
        }

    }

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        graph = new List[N + 1];
        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            graph[a].add(new Node(b, c, 0));
            graph[b].add(new Node(a, c, 0));
        }

        dist = new long[N + 1][K + 1];
        for (int i = 1; i <= N; i++) {
            Arrays.fill(dist[i], INF);
        }

        pq = new PriorityQueue<>();
    }

    private static void sol() throws IOException {
        pq.offer(new Node(1, 0, 0));
        dist[1][0] = 0;

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (cur.cost > dist[cur.to][cur.cnt]) {
                continue;
            }

            for (Node next : graph[cur.to]) {
                long nextCost = dist[cur.to][cur.cnt] + next.cost;

                // not exclude
                if (nextCost < dist[next.to][cur.cnt]) {
                    dist[next.to][cur.cnt] = nextCost;
                    pq.offer(new Node(next.to, nextCost, cur.cnt));
                }

                if (cur.cnt < K && cur.cost < dist[next.to][cur.cnt + 1]) {
                    dist[next.to][cur.cnt + 1] = cur.cost;
                    pq.offer(new Node(next.to, cur.cost, cur.cnt + 1));
                }
            }
        }

        long ans = INF;
        for (int i = 0; i <= K; i++) {
            ans = Math.min(ans, dist[N][i]);
        }
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```
