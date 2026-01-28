```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static PriorityQueue<Edge> pq;
    private static int[] uf, size;
    private static int N, M, S;

    public static void main(String[] args) throws IOException {
        init();

        int answer = kruskal();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        S = Integer.parseInt(st.nextToken());

        pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o1.w, o2.w));
        uf = new int[N+1];
        size = new int[N+1];

        for (int i = 1; i <= N; i++) {
            uf[i] = i;
            size[i] = 1;
        }

        for (int i = 1; i <= M; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());

            pq.add(new Edge(u, v, w));
        }

        st = new StringTokenizer(br.readLine());
    }

    private static int kruskal() {
        int cost = 0;
        int count = 0;

        while (!pq.isEmpty() && count < N-1) {
            Edge current = pq.poll();

            int root1 = find(current.u);
            int root2 = find(current.v);
            if (root1 == root2) continue;
            union(root1, root2);
            cost += current.w;
            count++;
        }

        return cost;
    }

    private static void union(int x, int y) {
        if (size[x] < size[y]) {
            uf[x] = y;
            size[y] += size[x];
        } else {
            uf[y] = x;
            size[x] += size[y];
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
