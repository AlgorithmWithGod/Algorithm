```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.ArrayList;
import java.util.List;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main {
    private static BufferedReader Br;
    private static BufferedWriter Bw;
    private static StringBuilder Sb;
    private static int N;
    private static int M;
    private static List<Node>[] Graph;

    private static class Node implements Comparable<Node> {
        int v;
        int w;
        public Node(int v, int w) {
            this.v = v;
            this.w = w;
        }
        @Override
        public int compareTo(Node o) {
            return this.w - o.w;
        }
    }

    public static void main(String[] args) throws IOException {
        Br = new BufferedReader(new InputStreamReader(System.in));
        Bw = new BufferedWriter(new OutputStreamWriter(System.out));
        Sb = new StringBuilder();
        StringTokenizer st = new StringTokenizer(Br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        Graph = new ArrayList[N + 1];
        for (int i = 1; i <= N; i++) {
            Graph[i] = new ArrayList<>();
        }
        for (int i = 0; i < N - 1; i++) {
            st = new StringTokenizer(Br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());
            Graph[a].add(new Node(b, w));
            Graph[b].add(new Node(a, w));
        }
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(Br.readLine());
            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            Sb.append(dijkstra(s, e)).append("\n");
        }
        Bw.write(Sb.toString());
        Bw.flush();
        Bw.close();
        Br.close();
    }

    private static int dijkstra(int start, int end) {
        int[] dist = new int[N + 1];
        for (int i = 1; i <= N; i++)
            dist[i] = Integer.MAX_VALUE;
        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.add(new Node(start, 0));
        dist[start] = 0;
        while (!pq.isEmpty()) {
            Node cur = pq.poll();
            if (dist[cur.v] < cur.w) continue;
            if (cur.v == end) return cur.w;

            for (Node next : Graph[cur.v]) {
                if (dist[next.v] > cur.w + next.w) {
                    dist[next.v] = cur.w + next.w;
                    pq.add(new Node(next.v, dist[next.v]));
                }
            }
        }
        return -1;
    }
}

```
