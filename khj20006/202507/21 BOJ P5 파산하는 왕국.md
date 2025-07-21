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
    static int[][] a;
    static boolean[] dp, vis;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        for(int T=io.nextInt(); T-->0;){
            init();
            solve();
        }

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        a = new int[N][N];
        dp = new boolean[1<<N];
        vis = new boolean[1<<N];
        for(int i=0;i<N;i++) for(int j=0;j<N;j++) a[i][j] = io.nextInt();

    }

    static void solve() throws Exception {

        dp[0] = true;
        vis[0] = true;
        int cnt = 0;
        for(int i=0;i<N;i++) {
            if(get(((1<<N)-1)^(1<<i))) {
                cnt++;
                io.write((i+1) + " ");
            }
        }
        if(cnt == 0) io.write("0");
        io.write("\n");

    }

    static boolean get(int k) {
        if(vis[k]) return dp[k];
        vis[k] = true;
        for(int i=0;i<N;i++) if((k & (1<<i)) != 0) {
            int p = k^(1<<i);
            int sum = 0;
            if(!get(p)) continue;
            for(int j=0;j<N;j++) if((p & (1<<j)) == 0) sum += a[i][j];
            if(sum > 0) return (dp[k] = true);
        }
        return dp[k];
    }

}
```
