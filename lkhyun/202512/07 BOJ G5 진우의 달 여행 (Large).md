```java
import java.util.*;
import java.io.*;
public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;

    static int N,M;
    static int[][] table;
    static int[][][] dp;
    public static void main(String[] args) throws Exception{
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        table = new int[N][M];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                table[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        dp = new int[N][M][3];

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                Arrays.fill(dp[i][j],Integer.MAX_VALUE);
            }
        }

        dp[0][0][1] = table[0][0];
        dp[0][0][2] = table[0][0];
        for (int i = 1; i < M-1; i++) {
            for (int j = 0; j < 3; j++) {
                dp[0][i][j] = table[0][i];
            }
        }
        dp[0][M-1][0] = table[0][M-1];
        dp[0][M-1][1] = table[0][M-1];

        for (int i = 1; i < N; i++) {
            dp[i][0][1] = dp[i-1][0][2] + table[i][0];
            dp[i][0][2] = Math.min(dp[i-1][1][0],dp[i-1][1][1]) + table[i][0];
            for (int j = 1; j < M-1; j++) {
                dp[i][j][0] = Math.min(dp[i-1][j-1][1],dp[i-1][j-1][2]) + table[i][j];
                dp[i][j][1] = Math.min(dp[i-1][j][0],dp[i-1][j][2]) + table[i][j];
                dp[i][j][2] = Math.min(dp[i-1][j+1][0],dp[i-1][j+1][1]) + table[i][j];
            }
            dp[i][M-1][0] = Math.min(dp[i-1][M-2][1],dp[i-1][M-2][2]) + table[i][M-1];
            dp[i][M-1][1] = dp[i-1][M-1][0] + table[i][M-1];
        }
        
        int ans = Integer.MAX_VALUE;
        for (int i = 0; i < M; i++) {
            for (int j = 0; j < 3; j++) {
                ans = Math.min(ans,dp[N-1][i][j]);
            }
        }
        bw.write(ans+"");
        bw.close();
    }
}
```
