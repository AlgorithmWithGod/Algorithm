```java
import java.io.*;
import java.util.*;

public class BJ_32294_수열과_개구리 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int   N;
    private static int[] pos, sec;
    private static long[]          dist;
    private static List<Integer>[] graph;
    private static Queue<Node>     pq;

    private static class Node implements Comparable<Node> {
        int  val;
        long cost;

        public Node(int val, long cost) {
            this.val = val;
            this.cost = cost;
        }

        @Override
        public int compareTo(Node o) {
            return Long.compare(cost, o.cost);
        }

    }

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        graph = new ArrayList[N + 2];
        for (int i = 0; i <= N + 1; i++) {
            graph[i] = new ArrayList<>();
        }

        pos = new int[N + 2];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            pos[i] = Integer.parseInt(st.nextToken());
            graph[Math.min(i + pos[i], N + 1)].add(i);
            graph[Math.max(i - pos[i], 0)].add(i);
        }

        sec = new int[N + 2];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            sec[i] = Integer.parseInt(st.nextToken());
        }

        dist = new long[N + 2];
        Arrays.fill(dist, Long.MAX_VALUE);
        dist[0] = 0;
        dist[N + 1] = 0;
        pq = new PriorityQueue<>();
    }

    private static void sol() throws IOException {
        pq.offer(new Node(0, 0));
        pq.offer(new Node(N + 1, 0));

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (cur.cost > dist[cur.val]) continue;

            for (int next : graph[cur.val]) {
                long newDist = sec[next] + cur.cost;

                if (newDist < dist[next]) {
                    dist[next] = newDist;
                    pq.offer(new Node(next, dist[next]));
                }
            }
        }

        for (int i = 1; i <= N; i++) {
            sb.append(dist[i]).append(" ");
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```