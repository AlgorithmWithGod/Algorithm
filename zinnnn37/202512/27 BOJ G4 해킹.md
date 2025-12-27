```java
import java.io.*;
import java.util.*;

public class BJ_10282_해킹 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int N, D, C;
    private static int[]        dist;
    private static Queue<Node>  pq;
    private static List<Node>[] graph;

    private static class Node implements Comparable<Node> {
        int to;
        int weight;

        Node(int to, int weight) {
            this.to = to;
            this.weight = weight;
        }

        @Override
        public int compareTo(Node o) {
            return Integer.compare(this.weight, o.weight);
        }

    }

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());

        while (T-- > 0) {
            init();
            sol();
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        D = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        graph = new List[N + 1];
        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        dist = new int[N + 1];
        Arrays.fill(dist, Integer.MAX_VALUE);

        pq = new PriorityQueue<>();
        for (int i = 0; i < D; i++) {
            st = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int s = Integer.parseInt(st.nextToken());

            graph[b].add(new Node(a, s));
        }

    }

    private static void sol() throws IOException {
        pq.offer(new Node(C, 0));
        dist[C] = 0;

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (cur.weight > dist[cur.to]) continue;

            for (Node next : graph[cur.to]) {
                int nextWeight = dist[cur.to] + next.weight;

                if (dist[next.to] > nextWeight) {
                    dist[next.to] = nextWeight;
                    pq.offer(new Node(next.to, nextWeight));
                }
            }
        }

        int cnt = 0;
        int max = 0;
        for (int i = 1; i <= N; i++) {
            if (dist[i] == Integer.MAX_VALUE) continue;

            cnt++;
            max = Math.max(max, dist[i]);
        }
        sb.append(cnt).append(" ").append(max).append("\n");
    }

}
```