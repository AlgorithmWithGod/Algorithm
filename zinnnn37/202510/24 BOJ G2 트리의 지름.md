```java
package etc;

import java.io.*;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_1167_트리의_지름 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int V, ans, max, maxNode;
    private static int[] dist;
    private static List<Node>[] graph;

    private static class Node {
        int to;
        int weight;

        Node(int to, int weight) {
            this.to = to;
            this.weight = weight;
        }
    }

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        V = Integer.parseInt(br.readLine());
        ans = 0;
        max = 0;
        maxNode = 0;

        dist = new int[V + 1];
        Arrays.fill(dist, -1);
        dist[1] = 0;

        graph = new List[V + 1];
        for (int i = 1; i <= V; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < V; i++) {
            st = new StringTokenizer(br.readLine());

            int v = Integer.parseInt(st.nextToken());

            int u;
            while ((u = Integer.parseInt(st.nextToken())) != -1) {
                int w = Integer.parseInt(st.nextToken());
                graph[v].add(new Node(u, w));
            }
        }
    }

    private static void sol() throws IOException {
        dfs(1, 0);
        findMax();

        max = 0;
        Arrays.fill(dist, -1);
        dist[maxNode] = 0;
        dfs(maxNode, 0);
        findMax();

        bw.write(max + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void dfs(int v, int w) throws IOException {
        for (Node u : graph[v]) {
            if (dist[u.to] != -1) continue;

            dist[u.to] = u.weight + w;
            dfs(u.to, dist[u.to]);
        }
    }

    private static void findMax() {
        for (int i = 1; i <= V; i++) {
            if (max < dist[i]) {
                max = Math.max(max, dist[i]);
                maxNode = i;
            }
        }
    }

}
```