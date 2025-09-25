```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = (int)1e8+5;
    private static List<Node>[] graph;
    private static List<Integer> answer;
    private static int[] dist1, dist2, dist3, input;
    private static int n, m, t, s, g, h, temp;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());

        while (T-->0) {
            init();
            dijkstra(g, dist1);
            dijkstra(h, dist2);
            dijkstra(s, dist3);

            for (int i = 0; i < t; i++) {
                int result = Math.min(dist1[s] + dist2[input[i]], dist1[input[i]] + dist2[s]);
                result += temp;
                if (result == dist3[input[i]]) {
                    answer.add(input[i]);
                }
            }

            Collections.sort(answer);

            for (int i = 0; i < answer.size()-1; i++) {
                bw.write(answer.get(i) + " ");
            }
            bw.write(answer.get(answer.size()-1) + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        t = Integer.parseInt(st.nextToken());

        graph = new List[n+1];
        dist1 = new int[n+1];
        dist2 = new int[n+1];
        dist3 = new int[n+1];
        input = new int[t];
        answer = new ArrayList<>();

        st = new StringTokenizer(br.readLine());
        s = Integer.parseInt(st.nextToken());
        g = Integer.parseInt(st.nextToken());
        h = Integer.parseInt(st.nextToken());

        for (int i = 0; i <= n; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());

            if ((a == g && b == h) || (a == h && b == g)) temp = cost;

            graph[a].add(new Node(b, cost));
            graph[b].add(new Node(a, cost));
        }

        for (int i = 0; i < t; i++) {
            input[i] = Integer.parseInt(br.readLine());
        }
    }

    private static void dijkstra(int start, int[] dist) {
        PriorityQueue<Node> pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o1.cost, o2.cost));
        Arrays.fill(dist, INF);
        dist[start] = 0;
        pq.add(new Node(start, dist[start]));

        while (!pq.isEmpty()) {
            Node current = pq.poll();

            if (current.cost > dist[current.dest]) continue;

            for (Node next : graph[current.dest]) {
                int nCost = dist[current.dest] + next.cost;

                if (nCost < dist[next.dest]) {
                    dist[next.dest] = nCost;
                    pq.add(new Node(next.dest, nCost));
                }
            }
        }
    }

    static class Node {
        int dest;
        int cost;

        public Node(int dest, int cost) {
            this.dest = dest;
            this.cost = cost;
        }
    }
}
```
