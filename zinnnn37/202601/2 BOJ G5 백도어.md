```java
import java.io.*;
import java.util.*;

public class BJ_17396_백도어 {

    private static final int  FALSE = 0;
    private static final int  TRUE  = 1;
    private static final long INF   = 100_000L * 1000_000 + 1;

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M;
    private static int[]        isVisible;
    private static long[]       dist;
    private static List<Node>[] graph;
    private static Queue<Node>  pq;

    private static class Node implements Comparable<Node> {
        int  to;
        long weight;

        public Node(int to, long weight) {
            this.to = to;
            this.weight = weight;
        }

        @Override
        public int compareTo(Node o) {
            return Long.compare(this.weight, o.weight);
        }

    }

    public static void main(String[] args) throws IOException {
        init();
        sol();

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        graph = new List[N];
        for (int i = 0; i < N; i++) {
            graph[i] = new ArrayList<>();
        }

        isVisible = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            isVisible[i] = Integer.parseInt(st.nextToken());
        }

        dist = new long[N];
        Arrays.fill(dist, INF);

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            graph[a].add(new Node(b, c));
            graph[b].add(new Node(a, c));
        }

        pq = new PriorityQueue<>();
    }

    private static void sol() throws IOException {
        pq.offer(new Node(0, 0));
        dist[0] = 0;

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (cur.to == N - 1) {
                bw.write(dist[cur.to] + "");
                return;
            }

            if (dist[cur.to] < cur.weight) continue;

            for (Node next : graph[cur.to]) {
                if (next.to != N - 1 && isVisible[next.to] == TRUE) continue;

                long newDist = dist[cur.to] + next.weight;

                if (newDist < dist[next.to]) {
                    dist[next.to] = newDist;
                    pq.offer(new Node(next.to, newDist));
                }
            }
        }
        bw.write("-1");
    }

}
```
