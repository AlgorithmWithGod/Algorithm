```java
import java.io.*;
import java.util.*;

class Edge implements Comparable<Edge> {
    int u, v, weight;

    public Edge(int u, int v, int weight) {
        this.u = u;
        this.v = v;
        this.weight = weight;
    }

    @Override
    public int compareTo(Edge o) {
        return this.weight - o.weight;
    }
}

public class Main {
    
    static int[] parent;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        while (true) {
            st = new StringTokenizer(br.readLine());
            int m = Integer.parseInt(st.nextToken());
            int n = Integer.parseInt(st.nextToken());

            if (m == 0 && n == 0) break;

            List<Edge> edges = new ArrayList<>();
            long totalCost = 0;

            for (int i = 0; i < n; i++) {
                st = new StringTokenizer(br.readLine());
                int u = Integer.parseInt(st.nextToken());
                int v = Integer.parseInt(st.nextToken());
                int w = Integer.parseInt(st.nextToken());
                edges.add(new Edge(u, v, w));
                totalCost += w;
            }

            Collections.sort(edges);

            parent = new int[m];
            for (int i = 0; i < m; i++) parent[i] = i;

            long mstCost = 0;
            int count = 0;

            for (Edge edge : edges) {
                if (find(edge.u) != find(edge.v)) {
                    union(edge.u, edge.v);
                    mstCost += edge.weight;
                    count++;
                    if (count == m - 1) break;
                }
            }

            System.out.println(totalCost - mstCost);
        }
    }

    static int find(int x) {
        if (parent[x] == x) return x;
        return parent[x] = find(parent[x]);
    }

    static void union(int x, int y) {
        x = find(x);
        y = find(y);
        if (x != y) parent[y] = x;
    }
}
```
