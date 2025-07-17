```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static int n, e;
    static List<List<Node>> list = new ArrayList<>();
    static final int INF = 987654321;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        e = Integer.parseInt(st.nextToken());

        for (int i = 0; i <= n; i++)
            list.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            list.get(from).add(new Node(to, cost));
            list.get(to).add(new Node(from, cost));
        }

        st = new StringTokenizer(br.readLine());
        int v1 = Integer.parseInt(st.nextToken());
        int v2 = Integer.parseInt(st.nextToken());

        int[] dist1 = dijkstra(1);
        int[] distv1 = dijkstra(v1);
        int[] distv2 = dijkstra(v2);

        int path1 = dist1[v1] + distv1[v2] + distv2[n];
        int path2 = dist1[v2] + distv2[v1] + distv1[n];

        if (dist1[v1] >= INF || distv1[v2] >= INF || distv2[n] >= INF) path1 = INF;
        if (dist1[v2] >= INF || distv2[v1] >= INF || distv1[n] >= INF) path2 = INF;

        int result = Math.min(path1, path2);

        if (result >= INF)
            System.out.println("-1");
        else System.out.println(result);
    }

    static int[] dijkstra(int start) {
        int[] dist = new int[n + 1];
        Arrays.fill(dist, INF);
        dist[start] = 0;

        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.offer(new Node(start, 0));

        while (!pq.isEmpty()) {
            Node cur = pq.poll();
            int now = cur.idx;

            if (cur.cost > dist[now]) continue;

            for (Node next : list.get(now)) {
                if (dist[next.idx] > dist[now] + next.cost) {
                    dist[next.idx] = dist[now] + next.cost;
                    pq.offer(new Node(next.idx, dist[next.idx]));
                }
            }
        }

        return dist;
    }

    public static class Node implements Comparable<Node> {
        int idx, cost;

        Node(int idx, int cost) {
            this.idx = idx;
            this.cost = cost;
        }

        @Override
        public int compareTo(Node o) {
            return Integer.compare(this.cost, o.cost);
        }
    }
}

```
