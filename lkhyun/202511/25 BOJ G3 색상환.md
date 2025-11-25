```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static int N,K;
    static int[][] dp;
    static int MOD = 1000000003;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        K = Integer.parseInt(br.readLine());
        dp = new int[N+1][K+1]; //N개의 색중 K개를 선택하는 경우의 수

        for(int i=0;i<=N;i++){
            dp[i][1] = i; //색 i를 칠하는 경우의 수 여기서 1개를 색칠하는 경우는 i개임.
            dp[i][0] = 1;
        }
        for(int i = 2;i<=N;i++){
            for(int j = 2;j<=K;j++){
                dp[i][j] = (dp[i-1][j] + dp[i-2][j-1]) % MOD;
            }
        }

        int ans = (dp[N-1][K] + dp[N-3][K-1]) % MOD;
        bw.write(ans+"");
        bw.close();
    }
}
```
