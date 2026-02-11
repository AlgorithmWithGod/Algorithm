```
import java.io.*;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static PriorityQueue<Edge> pq;
    private static int[] uf, size;
    private static int R, C;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());

        while (T-->0) {
            init();
            int answer = kruskal();
            bw.write(answer + "\n");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        pq = new PriorityQueue<>((o1, o2) -> Integer.compare(o1.w, o2.w));
        uf = new int[R*C];
        size = new int[R*C];

        for (int i = 0; i < R*C; i++) {
            uf[i] = i;
            size[i] = 1;
        }

        for (int i = 0; i < R; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < C-1; j++) {
                int cost = Integer.parseInt(st.nextToken());
//                System.out.println(i*C+j + ", " + (i*C+j+1));
                pq.add(new Edge(i*C+j, i*C+j+1, cost));
            }
        }

//        System.out.println();
        for (int i = 0; i < R-1; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < C; j++) {
                int cost = Integer.parseInt(st.nextToken());
//                System.out.println(i*C+j + ", " + ((i+1)*C+j));
                pq.add(new Edge(i*C+j, (i+1)*C+j, cost));
            }
        }
    }

    private static int kruskal() {
        int result = 0;
        int count = 0;

        while (!pq.isEmpty() || count < R*C-1) {
            Edge current = pq.poll();

            int root1 = find(current.u);
            int root2 = find(current.v);
            if (root1 == root2) continue;
            union(root1, root2);
            result += current.w;
            count++;
        }

        return result;
    }

    private static void union(int X, int Y) {
        if (size[X] < size[Y]) {
            uf[X] = Y;
            size[Y] += size[X];
        } else {
            uf[Y] = X;
            size[X] += size[Y];
        }
    }

    private static int find(int x) {
        if (x == uf[x]) return x;

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
