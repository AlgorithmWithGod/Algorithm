```java
import java.io.*;
import java.util.*;

public class BOJ16025 {

    static class DisjointSet {
        int[] root;
        DisjointSet(int size) {
            root = new int[size+1];
            for(int i=1;i<=size;i++) {
                root[i] = i;
            }
        }

        int find(int x) {
            return x == root[x] ? x : (root[x] = find(root[x]));
        }

        boolean union(int a, int b) {
            int x = find(a), y = find(b);
            if(x == y) {
                return false;
            }
            root[x] = y;
            return true;
        }
    }
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N, M, P, Q;
    static int[][] edges;
    static DisjointSet dsx, dsy;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        P = Integer.parseInt(st.nextToken());
        Q = Integer.parseInt(st.nextToken());

        edges = new int[P+Q][];
        long sum = 0;
        for(int i=0;i<P+Q;i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            int type = 0;
            if(i >= P) {
                type = 1;
                sum += (long)c * M;
            }
            else {
                sum += (long)c * N;
            }
            edges[i] = new int[]{a, b, c, type};
        }

        dsx = new DisjointSet(N);
        dsy = new DisjointSet(M);
        Arrays.sort(edges, (a,b) -> a[2]-b[2]);
        long X = N, Y = M;
        for(int[] edge : edges) {
            int a = edge[0], b = edge[1], type = edge[3];
            long c = edge[2];

            if(type == 0) {
                if(dsy.union(a, b)) {
                    sum -= c * X;
                    Y--;
                }
            }
            else {
                if(dsx.union(a, b)) {
                    sum -= c * Y;
                    X--;
                }
            }
        }

        bw.write(sum + "\n");
        bw.close();
    }
}
```
