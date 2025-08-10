```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, m;
    static List<List<Node>> list = new ArrayList<>();

    static class Node implements Comparable<Node> {
        int dest, cost;

        Node(int d, int c) {
            this.dest = d;
            this.cost = c;
        }

        @Override
        public int compareTo(Node o) {
            return this.cost - o.cost;
        }
    }

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());

        for (int i = 0; i < n + 1; i++) {
            list.add(new ArrayList<>());
        }

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());

            list.get(from).add(new Node(to, cost));
            list.get(to).add(new Node(from, cost));
        }

        dijkstra(1, n);
    }

    static void dijkstra(int start, int end) {
        int[] dist = new int[n + 1];
        Arrays.fill(dist, 987654321);

        PriorityQueue<Node> pq = new PriorityQueue<>();
        dist[start] = 0;
        pq.add(new Node(start, 0));

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (dist[cur.dest] < cur.cost) continue;

            for (Node next : list.get(cur.dest)) {
                if (dist[next.dest] > dist[cur.dest] + next.cost) {
                    dist[next.dest] = dist[cur.dest] + next.cost;
                    pq.add(new Node(next.dest, dist[next.dest]));
                }
            }
        }

        System.out.println(dist[end]);
    }

}

```
