```
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] trees, queries;
    private static int[] uf, size;
    private static int N, Q;

    public static void main(String[] args) throws IOException {
        init();
        unionFind();

        for (int[] query : queries) {
            if (uf[query[0]] == uf[query[1]]) bw.write("1" + "\n");
            else bw.write("0" + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        Q = Integer.parseInt(st.nextToken());

        trees = new int[N+1][3];
        queries = new int[Q][2];
        uf = new int[N+1];
        size = new int[N+1];


        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            trees[i][0] = x1;
            trees[i][1] = x2;
            trees[i][2] = i;

            uf[i] = i;
            size[i] = 1;
        }

        for (int i = 0; i < Q; i++) {
            st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());

            queries[i][0] = start;
            queries[i][1] = end;
        }

        Arrays.sort(trees, (o1, o2) -> {
            if (o1[0] == o2[0]) return Integer.compare(o1[1], o2[1]);
            return Integer.compare(o1[0], o2[0]);
        });
    }

    private static void unionFind() {
        int maxEnd = trees[1][1];
        int start = 1;

        for (int i = 2; i <= N; i++) {
            if (valid(maxEnd, trees[i][0])) {
                union(trees[start][2], trees[i][2]);
            } else {
                start = i;
            }
            maxEnd = Math.max(maxEnd, trees[i][1]);
        }
    }

    private static boolean valid(int x2, int x3) {
        return x2 >= x3;
    }

    private static void union(int x, int y) {
        int X = find(x);
        int Y = find(y);

        if (X == Y) return;

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
}
```
