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

    static int N, M, R;
    static long[][] dp;
    static boolean[][] vis;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();
    }

    public static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        dp = new long[N][1<<N];
        vis = new boolean[N][1<<N];
        R = io.nextInt()-1;
        int state = 0, last = R;
        for(int i=1;i<M;i++) {
            last = io.nextInt()-1;
            state |= (1<<last);
        }
        dp[last][state] = 1;
        vis[last][state] = true;

    }

    static void solve() throws Exception {

        io.write(get(R,(1<<N)-1) + "\n");

    }

    static long get(int n, int k) {
        if(dp[n][k] != 0 || vis[n][k]) return dp[n][k];
        vis[n][k] = true;
        int state = k | (1<<R);

        boolean can = false;
        boolean[] leftCan = new boolean[N];
        for(int i=(n+N-1)%N,x=0;x<N-1;x++) {
            int min = Math.min(i,n), max = Math.max(i,n);
            if(min+N-1 == max || max-min == 1) leftCan[i] = false;
            else leftCan[i] = can;
            if(!can) {
                if((state & (1<<i)) != 0) can = true;
            }
            i = (i+N-1)%N;
        }

        can = false;
        boolean[] rightCan = new boolean[N];
        for(int i=(n+1)%N,x=0;x<N-1;x++) {
            int min = Math.min(i,n), max = Math.max(i,n);
            if(min+N-1 == max || max-min == 1) rightCan[i] = false;
            else rightCan[i] = can;
            if(!can) {
                if((state & (1<<i)) != 0) can = true;
            }
            i = (i+1)%N;
        }

        for(int i=0;i<N;i++) if((k & (1<<i)) != 0 && leftCan[i] && rightCan[i]) {
            dp[n][k] += get(i, k^(1<<n));
        }

        return dp[n][k];
    }

}
```
