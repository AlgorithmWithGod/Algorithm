```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final long INF = Long.MAX_VALUE/2;
    private static List<Integer>[] graph;
    private static long[] dist;
    private static int[] a, b;
    private static int N;
    public static void main(String[] args) throws IOException {
        init();
        dijkstra();
        for (int i = 1; i <= N; i++) {
            bw.write(dist[i] + " ");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        a = new int[N+1];
        b = new int[N+1];
        dist = new long[N+1];
        graph = new List[N+1];

        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            a[i] = Integer.parseInt(st.nextToken());
            if (1 <= i-a[i] && i-a[i] <= N) {
                graph[i-a[i]].add(i);
            }

            if (1 <= i+a[i] && i+a[i] <= N) {
                graph[i+a[i]].add(i);
            }
        }

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            b[i] = Integer.parseInt(st.nextToken());
        }
    }

    private static void dijkstra() {
        PriorityQueue<Node> pq = new PriorityQueue<>((o1, o2) -> Long.compare(o1.cost, o2.cost));
        Arrays.fill(dist, INF);
        for (int i = 1; i <= N; i++) {
            if (i-a[i] < 1 || i+a[i] > N) {
                dist[i] = b[i];
                pq.add(new Node(i, b[i]));
            }
        }

        while (!pq.isEmpty()) {
            Node current = pq.poll();

            if (current.cost > dist[current.dest]) continue;

            for (int nDest : graph[current.dest]) {
                long nCost = current.cost + b[nDest];

                if (nCost < dist[nDest]) {
                    dist[nDest] = nCost;
                    pq.add(new Node(nDest, dist[nDest]));
                }
            }
        }
    }

    static class Node {
        int dest;
        long cost;

        public Node(int dest, long cost) {
            this.dest = dest;
            this.cost = cost;
        }
    }
}
```
