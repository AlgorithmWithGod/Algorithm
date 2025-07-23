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
    static int[] arr;
    static boolean[][][][] dp;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    static void init() throws Exception {

        N = io.nextInt();
        arr = new int[N];
        for(int i=0;i<N;i++) arr[i] = io.nextInt();
        dp = new boolean[71][71][71][71];

    }

    static void solve() throws Exception {

        dp[0][0][0][0] = true;
        for(int i=0;i<N;i++) {
            boolean[][][][] ndp = new boolean[71][71][71][71];
            for(int a=0;a<=70;a++) for(int b=0;b<=70;b++) for(int c=0;c<=70;c++) for(int d=0;d<=70;d++) if(dp[a][b][c][d]){
                if(a+arr[i] <= 70) ndp[a+arr[i]][b][c][d] = true;
                if(b+arr[i] <= 70) ndp[a][b+arr[i]][c][d] = true;
                if(c+arr[i] <= 70) ndp[a][b][c+arr[i]][d] = true;
                if(d+arr[i] <= 70) ndp[a][b][c][d+arr[i]] = true;
            }
            for(int a=0;a<=70;a++) for(int b=0;b<=70;b++) for(int c=0;c<=70;c++) for(int d=0;d<=70;d++) {
                ndp[a][b][c][d] |= dp[a][b][c][d];
            }
            dp = ndp;

        }
        int ans = -1;
        for(int i=1;i<=70;i++) for(int j=1;j<=70;j++) {
            if(dp[i][i][j][j]) ans = Math.max(ans, i*j);
        }
        io.write(ans + "\n");

    }

}
```
