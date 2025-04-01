```java
import java.util.*;
import java.io.*;
import java.awt.Point;
public class Main {

    static int N, M;
    static Point[] points;
    static int[] parents;
    static PriorityQueue<Edge> pq;

    static class Edge implements Comparable<Edge>{
        int from, to;
        double wt;
        public Edge(int from, int to, double wt) {
            this.from = from;
            this.to = to;
            this.wt = wt;
        }

        @Override
        public int compareTo(Edge o) {
            return Double.compare(this.wt, o.wt);
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken()); // 정점의 개수
        M = Integer.parseInt(st.nextToken()); // 이미 연결된 통로의 개수

        points = new Point[N+1];
        for (int i = 1; i < N+1; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            points[i] = new Point(x, y);
        }

        makeSet();

        for (int i = 0; i < M; i++) {
            // 이미 연결된 정점들에 대해 union
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            union(a, b);
        }

        makePQ();
        double result = kruskal();
        System.out.printf("%.2f\n", result);
        br.close();
    }

    static double kruskal() {
        double result = 0.0;
        while (!pq.isEmpty()) {
            Edge e = pq.poll();
            if (union(e.to, e.from)) {
                result += e.wt;
            }
        }
        return result;
    }

    static void makePQ() {
        pq = new PriorityQueue<>();
        for (int i = 1; i < N; i++) {
            for (int j = i+1; j < N+1; j++) {
                pq.add(new Edge(i, j, getDist(points[i], points[j])));
            }
        }
    }

    static void makeSet() {
        parents = new int[N+1];
        for (int i = 1; i < N+1; i++) {
            parents[i] = i;
        }
    }

    static int find(int a) {
        if (parents[a] == a) return a;
        return parents[a] = find(parents[a]);
    }

    static boolean union(int a, int b) {
        int aRoot = find(a);
        int bRoot = find(b);
        if (aRoot == bRoot) return false;
        if (aRoot < bRoot) {
            parents[bRoot] = aRoot;
        } else {
            parents[bRoot] = aRoot;
        }
        return true;
    }

    static double getDist(Point a, Point b) {
        return Math.sqrt(Math.pow(a.x - b.x, 2) + Math.pow(a.y - b.y, 2));
    }
}

```
