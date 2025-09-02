```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main {
    private static BufferedReader br;
    private static int n;
    private static int m;
    private static char[] genders;
    private static ArrayList<Edge>[] graph;

    private static class Edge implements Comparable<Edge> {
        int v;
        int w;
        public Edge(int v, int w) {
            this.v = v;
            this.w = w;
        }
        @Override
        public int compareTo(Edge o) {
            return this.w - o.w;
        }
    }

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        genders = new char[n + 1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= n; i++) {
            genders[i] = st.nextToken().charAt(0);
        }
        graph = new ArrayList[n + 1];
        for (int i = 1; i <= n; i++) {
            graph[i] = new ArrayList<>();
        }
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());
            //같은 성별 노드는 연결하지 않음
            if (genders[u] == genders[v]) continue;
            graph[u].add(new Edge(v, w));
            graph[v].add(new Edge(u, w));
        }

        int answer = prim();
        System.out.println(answer);
    }

    private static int prim() {
        boolean[] visited = new boolean[n + 1];
        PriorityQueue<Edge> pq = new PriorityQueue<>();
        int total = 0;
        int count = 0;
        visited[1] = true;
        count++;
        for (Edge e : graph[1]) {
            pq.add(e);
        }

        while (!pq.isEmpty()) {
            Edge cur = pq.poll();
            if (visited[cur.v]) continue;
            visited[cur.v] = true;
            total += cur.w;
            count++;
            for (Edge next : graph[cur.v]) {
                if (!visited[next.v]) {
                    pq.add(next);
                }
            }
        }

        if (count == n) {
            return total;
        } else {
            return -1;
        }
    }
}

```
