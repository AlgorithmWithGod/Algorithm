```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static PriorityQueue<Long>[] dist;
    private static List<Node>[] graph;
    private static int n, m, k;

    public static void main(String[] args) throws IOException {
        init();
        dijkstra();

        for (int i = 1; i <= n; i++) {
            if (dist[i].size() < k) {
                bw.write("-1" + "\n");
            } else {
                bw.write(dist[i].peek() + "\n");
            }
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        k = Integer.parseInt(st.nextToken());

        dist = new PriorityQueue[n+1];
        graph = new List[n+1];

        for (int i = 0; i <= n; i++) {
            dist[i] = new PriorityQueue<>((o1, o2) -> Long.compare(o2, o1));
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            long c = Long.parseLong(st.nextToken());

            graph[a].add(new Node(b, c));
        }
    }

    private static void dijkstra() {
        PriorityQueue<Node> pq = new PriorityQueue<>((o1, o2) -> Long.compare(o1.cost, o2.cost));
        dist[1].add(0L);
        pq.add(new Node(1, 0L));

        while (!pq.isEmpty()) {
            Node current = pq.poll();

            for (Node next : graph[current.dest]) {
                long nCost = current.cost + next.cost;
                if (dist[next.dest].size() < k) {
                    dist[next.dest].add(nCost);
                    pq.add(new Node(next.dest, nCost));
                } else if (dist[next.dest].peek() > nCost) {
                    dist[next.dest].poll();
                    dist[next.dest].add(nCost);
                    pq.add(new Node(next.dest, nCost));
                }
            }
        }
    }

    static class Node {
        int dest;
        long cost;

        Node (int dest, long cost) {
            this.dest = dest;
            this.cost = cost;
        }
    }
}
```
