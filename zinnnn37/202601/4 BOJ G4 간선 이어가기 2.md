```java
import java.io.*;
import java.util.*;

public class BJ_14284_간선_이어가기_2 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M, S, T;
    private static int[]        dist;
    private static List<Node>[] graph;
    private static Queue<Node>  q;

    private static class Node implements Comparable<Node> {
        int to;
        int weight;

        public Node(int to, int weight) {
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

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        graph = new List[N + 1];
        for (int i = 1; i <= N; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            graph[a].add(new Node(b, c));
            graph[b].add(new Node(a, c));
        }

        st = new StringTokenizer(br.readLine());
        S = Integer.parseInt(st.nextToken());
        T = Integer.parseInt(st.nextToken());

        dist = new int[N + 1];
        Arrays.fill(dist, 987654321);
        q = new PriorityQueue<>();
    }

    private static void sol() throws IOException {
        q.offer(new Node(S, 0));
        dist[S] = 0;

        while (!q.isEmpty()) {
            Node cur = q.poll();

            if (dist[cur.to] < cur.weight) continue;

            if (cur.to == T) {
                bw.write(cur.weight + "");
                return;
            }

            for (Node next : graph[cur.to]) {
                int newDist = dist[cur.to] + next.weight;

                if (newDist < dist[next.to]) {
                    dist[next.to] = newDist;
                    q.offer(new Node(next.to, newDist));
                }
            }
        }
    }

}
```
