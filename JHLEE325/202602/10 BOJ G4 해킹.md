```java
import java.io.*;
import java.util.*;

class Node implements Comparable<Node> {
    int target, time;

    public Node(int target, int time) {
        this.target = target;
        this.time = time;
    }

    @Override
    public int compareTo(Node o) {
        return this.time - o.time;
    }
}

public class Main {
    
    static final int INF = Integer.MAX_VALUE;
    static List<Node>[] adj;
    static int[] dist;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            st = new StringTokenizer(br.readLine());
            int n = Integer.parseInt(st.nextToken());
            int d = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            adj = new ArrayList[n + 1];
            for (int i = 1; i <= n; i++) adj[i] = new ArrayList<>();

            for (int i = 0; i < d; i++) {
                st = new StringTokenizer(br.readLine());
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                int s = Integer.parseInt(st.nextToken());
                adj[b].add(new Node(a, s));
            }

            dijkstra(c, n);
        }
    }

    static void dijkstra(int start, int n) {
        PriorityQueue<Node> pq = new PriorityQueue<>();
        dist = new int[n + 1];
        Arrays.fill(dist, INF);

        dist[start] = 0;
        pq.add(new Node(start, 0));

        while (!pq.isEmpty()) {
            Node curr = pq.poll();

            if (curr.time > dist[curr.target]) continue;

            for (Node next : adj[curr.target]) {
                if (dist[next.target] > dist[curr.target] + next.time) {
                    dist[next.target] = dist[curr.target] + next.time;
                    pq.add(new Node(next.target, dist[next.target]));
                }
            }
        }

        int count = 0;
        int maxTime = 0;
        for (int i = 1; i <= n; i++) {
            if (dist[i] != INF) {
                count++;
                maxTime = Math.max(maxTime, dist[i]);
            }
        }
        System.out.println(count + " " + maxTime);
    }
}
```
