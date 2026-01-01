```java
import java.io.*;
import java.util.*;

public class BJ_2211_네트워크_복구 {

    private static final int INF = 987654321;

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int N, M;
    private static int[] dist, parents;
    private static List<Node>[] graph;
    private static Queue<Node>  pq;
    private static Set<String>  set;

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
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        graph = new List[N + 1];
        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        dist = new int[N + 1];
        Arrays.fill(dist, INF);

        parents = new int[N + 1];

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            graph[a].add(new Node(b, c));
            graph[b].add(new Node(a, c));
        }

        pq = new PriorityQueue<>();
        set = new HashSet<>();
    }

    private static void sol() throws IOException {
        pq.offer(new Node(1, 0));
        dist[1] = 0;

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (cur.weight > dist[cur.to]) continue;

            for (Node next : graph[cur.to]) {
                int nextWeight = next.weight + dist[cur.to];

                if (nextWeight < dist[next.to]) {
                    dist[next.to] = nextWeight;
                    parents[next.to] = cur.to;
                    pq.offer(new Node(next.to, nextWeight));
                }
            }
        }

        getAns();
    }

    private static void getAns() throws IOException {
        for (int i = 1; i <= N; i++) {
            if (parents[i] == 0) continue;

            int min = Math.min(i, parents[i]);
            int max = Math.max(i, parents[i]);

            set.add(min + " " + max);
        }

        sb.append(set.size()).append("\n");
        for (String s : set) {
            sb.append(s).append("\n");
        }

        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```
