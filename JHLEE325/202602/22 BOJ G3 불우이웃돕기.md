```java
import java.io.*;
import java.util.*;

public class Main {

    static int[] parent;

    static class Edge implements Comparable<Edge> {
        int u, v, w;
        Edge(int u, int v, int w) {
            this.u = u;
            this.v = v;
            this.w = w;
        }
        @Override
        public int compareTo(Edge o) {
            return this.w - o.w;
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int N = Integer.parseInt(br.readLine());

        List<Edge> edges = new ArrayList<>();
        long totalLength = 0;

        for (int i = 0; i < N; i++) {
            String line = br.readLine();
            for (int j = 0; j < N; j++) {
                char c = line.charAt(j);
                int len = charToInt(c);

                if (len > 0) {
                    totalLength += len;
                    if (i != j) {
                        edges.add(new Edge(i, j, len));
                    }
                }
            }
        }

        Collections.sort(edges);

        parent = new int[N];
        for (int i = 0; i < N; i++) parent[i] = i;

        int useEdgeCount = 0;
        long mstSum = 0;

        for (Edge edge : edges) {
            if (union(edge.u, edge.v)) {
                mstSum += edge.w;
                useEdgeCount++;
            }
        }

        if (useEdgeCount == N - 1) {
            System.out.println(totalLength - mstSum);
        } else {
            System.out.println(-1);
        }
    }

    static int charToInt(char c) {
        if (c >= 'a' && c <= 'z') return c - 'a' + 1;
        if (c >= 'A' && c <= 'Z') return c - 'A' + 27;
        return 0;
    }

    static int find(int x) {
        if (parent[x] == x) return x;
        return parent[x] = find(parent[x]);
    }

    static boolean union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            parent[rootX] = rootY;
            return true;
        }
        return false;
    }
}
```
