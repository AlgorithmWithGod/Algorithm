```java
import java.io.*;
import java.util.*;

public class Main {

    static class node {
        double x, y;

        public node(double x, double y) {
            this.x = x;
            this.y = y;
        }
    }

    static class edge implements Comparable<edge> {
        int from, to;
        double weight;

        public edge(int from, int to, double weight) {
            this.from = from;
            this.to = to;
            this.weight = weight;
        }

        @Override
        public int compareTo(edge o) {
            return Double.compare(this.weight, o.weight);
        }
    }

    static int[] parent;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        node[] stars = new node[n];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            double x = Double.parseDouble(st.nextToken());
            double y = Double.parseDouble(st.nextToken());
            stars[i] = new node(x, y);
        }

        List<edge> edges = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                double dist = Math.sqrt(Math.pow(stars[i].x - stars[j].x, 2) + Math.pow(stars[i].y - stars[j].y, 2));
                edges.add(new edge(i, j, dist));
            }
        }

        Collections.sort(edges);

        parent = new int[n];
        for (int i = 0; i < n; i++) parent[i] = i;

        double result = 0;
        int cnt = 0;
        for (edge e : edges) {
            if (union(e.from, e.to)) {
                result += e.weight;
                cnt++;
                if (cnt == n - 1) break;
            }
        }

        System.out.printf("%.2f\n", result);
    }

    static int find(int x) {
        if (parent[x] == x) return x;
        return parent[x] = find(parent[x]);
    }

    static boolean union(int a, int b) {
        a = find(a);
        b = find(b);
        if (a == b) return false;
        parent[b] = a;
        return true;
    }
}
```
