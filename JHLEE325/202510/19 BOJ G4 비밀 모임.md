```java
import java.io.*;
import java.util.*;

public class Main {

    static class Node implements Comparable<Node> {
        int to, cost;

        public Node(int t, int c) {
            this.to = t;
            this.cost = c;
        }

        @Override
        public int compareTo(Node o) {
            return this.cost - o.cost;
        }
    }

    static final int INF = 987654321;
    static List<Node>[] graph;
    static int N, M, K;
    static int[] friends;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine());
        StringBuilder sb = new StringBuilder();

        while (T-- > 0) {
            st = new StringTokenizer(br.readLine());
            N = Integer.parseInt(st.nextToken());
            M = Integer.parseInt(st.nextToken());

            graph = new ArrayList[N + 1];
            for (int i = 1; i <= N; i++) graph[i] = new ArrayList<>();

            for (int i = 0; i < M; i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                int d = Integer.parseInt(st.nextToken());
                graph[a].add(new Node(b, d));
                graph[b].add(new Node(a, d));
            }

            K = Integer.parseInt(br.readLine());
            friends = new int[K];
            st = new StringTokenizer(br.readLine());
            for (int i = 0; i < K; i++) friends[i] = Integer.parseInt(st.nextToken());

            int[][] dist = new int[K][N + 1];
            for (int i = 0; i < K; i++) {
                dist[i] = dijkstra(friends[i]);
            }

            int minSum = INF;
            int room = 0;

            for (int i = 1; i <= N; i++) {
                int total = 0;
                for (int j = 0; j < K; j++) {
                    total += dist[j][i];
                }

                if (total < minSum) {
                    minSum = total;
                    room = i;
                }
            }

            sb.append(room).append('\n');
        }

        System.out.print(sb.toString());
    }

    public static int[] dijkstra(int start) {
        boolean[] check = new boolean[N + 1];
        int[] dist = new int[N + 1];

        Arrays.fill(dist, 987654321);
        dist[start] = 0;

        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.offer(new Node(start, 0));

        while (!pq.isEmpty()) {
            int cur = pq.poll().to;

            if (check[cur])
                continue;
            check[cur] = true;

            for (Node next : graph[cur]) {
                if (dist[next.to] > dist[cur] + next.cost) {
                    dist[next.to] = dist[cur] + next.cost;
                    pq.offer(new Node(next.to, dist[next.to]));
                }
            }
        }

        return dist;
    }
}```
