```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static class Point {
        double r;
        double c;
        public Point (double r, double c) {
            this.r = r;
            this.c = c;
        }
    }

    static class Edge implements Comparable<Edge>{
        int from;
        int to;
        double weight;
        public Edge(int from, int to, double weight) {
            this.from = from;
            this.to = to;
            this.weight = weight;
        }

        @Override
        public int compareTo(Edge o) {
            return Double.compare(this.weight, o.weight);
        }
    }
    static int n;
    static int[] parents;
    static Point[] points;
    static PriorityQueue<Edge> pq;


    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        points = new Point[n];
        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            double r = Double.parseDouble(st.nextToken());
            double c = Double.parseDouble(st.nextToken());
            points[i] = new Point(r, c);
        }
        // 자기 자신을 포함하는 부분집합 구성
        makeSet();
        // Point간의 거리를 계산해서 PQ에 등록
        pq = new PriorityQueue<>();
        for (int i = 0; i < n-1; i++) {
            for (int j = i+1; j < n; j++) {
                pq.offer(new Edge(i, j, getDist(points[i], points[j])));
            }
        }
        // ans: 별자리를 만드는 최소 비용
        double ans = 0.0;
        int edgeCnt = 0; // Kruskal 알고리즘은 간선이 n-1개 선택되면 종료
        while (!pq.isEmpty() && edgeCnt < n-1) {
            Edge e = pq.poll();
            if (union(e.from, e.to)) { // from, to가 서로소 집합에 속한다면 ans에 비용 추가
                ans += e.weight;
                edgeCnt++;
            }
        }
        System.out.printf("%.2f\n", ans);
        br.close();
    }

    private static void makeSet() {
        parents = new int[n];
        for (int i = 0; i < n; i++) {
            parents[i] = i;
        }
    }

    private static int find(int a) {
        if (a == parents[a]) return a;
        return parents[a] = find(parents[a]);
    }

    private static boolean union(int a, int b) {
        int aRoot = find(a);
        int bRoot = find(b);
        if (aRoot == bRoot) return false;
        if (aRoot < bRoot) {
            parents[bRoot] = aRoot;
        } else {
            parents[aRoot] = bRoot;
        }
        return true;
    }

    private static double getDist(Point x, Point y) {
        return Math.sqrt(Math.pow(x.r - y.r, 2) + Math.pow(x.c - y.c, 2));
    }
}

```
