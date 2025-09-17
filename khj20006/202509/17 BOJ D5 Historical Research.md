```java
import java.io.*;
import java.util.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens())
            nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

public class Main {

    static IOController io;

    //

    static int N, Q, bucketSize;
    static int[] a, origin;
    static int[][] queries;
    static long[] seg;

    public static void update(int s, int e, int i, long v, int n) {
        if(s == e) {
            seg[n] += v;
            return;
        }
        int m = (s+e)>>1;
        if(i <= m) update(s,m,i,v,n*2);
        else update(m+1,e,i,v,n*2+1);
        seg[n] = Math.max(seg[n*2], seg[n*2+1]);
    }

    public static void main(String[] args) throws Exception {

        io = new IOController();

        N = io.nextInt();
        Q = io.nextInt();
        bucketSize = (int)Math.sqrt(N);
        a = new int[N];
        int[][] tmp = new int[N][];
        origin = new int[N];

        for(int i=0;i<N;i++) {
            a[i] = io.nextInt();
            tmp[i] = new int[]{a[i], i};
        }

        Arrays.sort(tmp, (c,d) -> c[0]-d[0]);
        int value = 0, prev = tmp[0][0];
        origin[0] = prev;
        for(int i=0;i<N;i++) {
            int v = tmp[i][0], x = tmp[i][1];
            if(prev != v) value++;
            a[x] = value;
            origin[value] = v;
            prev = v;
        }

        queries = new int[Q][];
        for(int i=0;i<Q;i++) {
            int s = io.nextInt()-1;
            int e = io.nextInt()-1;
            queries[i] = new int[]{s,e,i};
        }

        Arrays.sort(queries, (c,d) -> {
            if(c[0] / bucketSize == d[0] / bucketSize) {
                return c[1]-d[1];
            }
            return c[0] / bucketSize - d[0] / bucketSize;
        });

        long[] ans = new long[Q];
        seg = new long[524288];
        int s = 0, e = -1;
        for(int i=0;i<Q;i++) {
            int ns = queries[i][0];
            int ne = queries[i][1];
            int idx = queries[i][2];

            while(s < ns) {
                int val = a[s];
                int org = origin[val];
                update(0,100001,val,-org,1);
                s++;
            }
            while(ns < s) {
                int val = a[--s];
                int org = origin[val];
                update(0,100001,val,org,1);
            }
            while(e < ne) {
                int val = a[++e];
                int org = origin[val];
                update(0,100001,val,org,1);
            }
            while(ne < e) {
                int val = a[e];
                int org = origin[val];
                update(0,100001,val,-org,1);
                e--;
            }

            ans[idx] = seg[1];

        }

        for(int i=0;i<Q;i++) io.write(ans[i] + "\n");

        io.close();

    }

}
```
