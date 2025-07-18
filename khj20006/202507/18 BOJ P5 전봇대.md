```java
import java.util.*;
import java.io.*;

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
        while (!st.hasMoreTokens()) nextLine();
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

    static int N;
    static long[] a;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        a = new long[N];
        for(int i=0;i<N;i++) a[i] = io.nextInt();

    }

    static void solve() throws Exception {

        long s = 1, e = 1000000000, m1 = s + (e-s)/3, m2 = s + (e-s)*2/3;
        while(e-s > 5) {
            long res1 = getDist(m1);
            long res2 = getDist(m2);
            if(res1 > res2) s = m1;
            else e = m2;
            m1 = s + (e-s)/3;
            m2 = s + (e-s)*2/3;
        }
        long ans = Long.MAX_VALUE;
        for(int k=(int)s;k<=e;k++) ans = Math.min(ans, getDist(k));
        io.write(ans + "\n");

    }

    static long getDist(long x) {
        long res = 0;
        for(int i=1;i<N;i++) res += Math.abs(x*i - a[i]);
        return res;
    }

}
```
