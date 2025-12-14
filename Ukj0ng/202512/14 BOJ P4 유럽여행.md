```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static PriorityQueue<Edge> edges;
    private static int[] arr, uf, size;
    private static int N, P, cost;

    public static void main(String[] args) throws IOException {
        init();
        int answer = MST(cost);

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        P = Integer.parseInt(st.nextToken());
        cost = 1001;

        arr = new int[N+1];
        uf = new int[N+1];
        size = new int[N+1];

        for (int i = 1; i <= N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
            cost = Math.min(cost, arr[i]);
            uf[i] = i;
            size[i] = 1;
        }

        edges = new PriorityQueue<>((o1, o2) -> Integer.compare(o1.w, o2.w));

        for (int i = 0; i < P; i++) {
            st = new StringTokenizer(br.readLine());
            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            int l = Integer.parseInt(st.nextToken());

            edges.add(new Edge(s, e, l*2 + arr[s] + arr[e]));
        }
    }

    private static int MST(int cost) {
        int count = 0;

        while (count < N && !edges.isEmpty()) {
            Edge edge = edges.poll();

            int root1 = find(edge.u);
            int root2 = find(edge.v);

            if (root1 == root2) continue;
            union(edge.u, edge.v);
            cost += edge.w;
            count++;
        }

        return cost;
    }

    private static void union(int x, int y) {
        int X = find(x);
        int Y = find(y);

        if (size[X] < size[Y]) {
            uf[X] = Y;
            size[Y] += size[X];
        } else {
            uf[Y] = X;
            size[X] += size[Y];
        }
    }

    private static int find(int x) {
        if (uf[x] == x) return x;

        return uf[x] = find(uf[x]);
    }

    static class Edge {
        int u;
        int v;
        int w;

        public Edge(int u, int v, int w) {
            this.u = u;
            this.v = v;
            this.w = w;
        }
    }
}
```
