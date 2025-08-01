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

    static int N, M, K;
    static int[][] UL, UR, DL, DR;
    static boolean[][] res;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        K = io.nextInt();
        UL = new int[N+2][M+2];
        UR = new int[N+2][M+2];
        DL = new int[N+2][M+2];
        DR = new int[N+2][M+2];
        res = new boolean[N+2][M+2];
        while(K-->0) {
            int x = io.nextInt();
            int y = io.nextInt();
            int w = io.nextInt();
            UL[x][y] = w+1;
            UR[x][y] = w+1;
            DL[x][y] = w+1;
            DR[x][y] = w+1;
        }

    }

    static void solve() throws Exception {

        for(int i=1;i<=N;i++) for(int j=1;j<=M;j++) {
            if(UR[i][j] > 0) {
                res[i][j] = true;
                UR[i+1][j] = Math.max(UR[i+1][j], UR[i][j]-1);
                UR[i][j+1] = Math.max(UR[i][j+1], UR[i][j]-1);
            }
        }

        for(int i=1;i<=N;i++) for(int j=M;j>=1;j--) {
            if(UL[i][j] > 0) {
                res[i][j] = true;
                UL[i+1][j] = Math.max(UL[i+1][j], UL[i][j]-1);
                UL[i][j-1] = Math.max(UL[i][j-1], UL[i][j]-1);
            }
        }

        for(int i=N;i>=1;i--) for(int j=1;j<=M;j++) {
            if(DR[i][j] > 0) {
                res[i][j] = true;
                DR[i-1][j] = Math.max(DR[i-1][j], DR[i][j]-1);
                DR[i][j+1] = Math.max(DR[i][j+1], DR[i][j]-1);
            }
        }

        for(int i=N;i>=1;i--) for(int j=M;j>=1;j--) {
            if(DL[i][j] > 0) {
                res[i][j] = true;
                DL[i-1][j] = Math.max(DL[i-1][j], DL[i][j]-1);
                DL[i][j-1] = Math.max(DL[i][j-1], DL[i][j]-1);
            }
        }

        int ans = 0;
        for(int i=1;i<=N;i++) for(int j=1;j<=M;j++) ans += res[i][j] ? 1 : 0;
        io.write(ans + "\n");

    }

}
```
