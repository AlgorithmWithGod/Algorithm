```java
import java.io.*;
import java.util.*;

public class BJ_1939_중량제한 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M, start, end;
    private static int[]        maxWeight;
    private static List<Node>[] graph;
    private static Queue<Node>  pq;

    private static class Node implements Comparable<Node> {
        int to;
        int weight;

        public Node(int to, int weight) {
            this.to = to;
            this.weight = weight;
        }

        @Override
        public int compareTo(Node o) {
            return Integer.compare(o.weight, this.weight);
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

        for (int i = 1; i <= M; i++) {
            st = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            graph[a].add(new Node(b, c));
            graph[b].add(new Node(a, c));
        }

        maxWeight = new int[N + 1];

        st = new StringTokenizer(br.readLine());
        start = Integer.parseInt(st.nextToken());
        end = Integer.parseInt(st.nextToken());
        maxWeight[start] = Integer.MAX_VALUE;

        pq = new PriorityQueue<>();
    }

    private static void sol() throws IOException {
        pq.offer(new Node(start, Integer.MAX_VALUE));

        while (!pq.isEmpty()) {
            Node cur = pq.poll();

            if (cur.to == end) {
                bw.write(String.valueOf(cur.weight));
                bw.flush();
                bw.close();
                br.close();
                return;
            }

            if (cur.weight < maxWeight[cur.to]) {
                continue;
            }

            for (Node next : graph[cur.to]) {
                int newWeight = Math.min(cur.weight, next.weight);

                if (newWeight > maxWeight[next.to]) {
                    maxWeight[next.to] = newWeight;
                    pq.offer(new Node(next.to, newWeight));
                }
            }
        }
    }

}
```