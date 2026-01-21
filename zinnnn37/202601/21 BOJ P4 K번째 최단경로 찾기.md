```java
import java.io.*;
import java.util.*;

public class BJ_1854_k번째_최단경로_찾기 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int N, M, K;
    private static List<Node>[]     graph;
    private static Queue<Node>      pq;
    private static Queue<Integer>[] dist;

    private static class Node implements Comparable<Node> {
        int to;
        int weight;

        public Node(int to, int weight) {
            this.to = to;
            this.weight = weight;
        }

        @Override
        public int compareTo(Node o) {
            return Integer.compare(this.weight, o.weight);
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
        for (int i = 1; i < N + 1; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            graph[a].add(new Node(b, c));
        }

        dist = new Queue[N + 1];
        for (int i = 1; i < N + 1; i++) {
            dist[i] = new PriorityQueue<>((a, b) -> b - a);
        }

        pq = new PriorityQueue<>();
    }

    private static void sol() throws IOException {
        pq.offer(new Node(1, 0));
        dist[1].offer(0);

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            for (Node next : graph[cur.to]) {
                int nextDist = cur.weight + next.weight;

                if (dist[next.to].size() == K && nextDist < dist[next.to].peek()) {
                    pq.offer(new Node(next.to, nextDist));
                    dist[next.to].poll();
                    dist[next.to].add(nextDist);
                } else if (dist[next.to].size() < K) {
                    pq.offer(new Node(next.to, nextDist));
                    dist[next.to].offer(nextDist);
                }
            }
        }

        for (int i = 1; i <= N; i++) {
            sb.append(dist[i].size() < K ? "-1" : dist[i].peek()).append("\n");
        }

        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```
