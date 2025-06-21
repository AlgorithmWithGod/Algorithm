```java
import java.io.*;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N;
    static int[][][] dp;
    static int MOD = 1000000000;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());
        //dp[자릿수][끝자리수][포함관계]
        dp = new int[N+1][10][1024];
        for (int i = 1; i <= 9; i++) {
            dp[1][i][1<<i] = 1;
        }

        for (int i = 2; i <= N; i++) {
            for (int j = 0; j <= 9; j++) {
                for (int k = 0; k < (1<<10); k++) {
                    if(j>0 && dp[i-1][j-1][k] > 0){
                        dp[i][j][k | 1<<j] += dp[i-1][j-1][k];
                        dp[i][j][k | 1<<j] %= MOD;
                    }
                    if(j<9 && dp[i-1][j+1][k] > 0){
                        dp[i][j][k | 1<<j] += dp[i-1][j+1][k];
                        dp[i][j][k | 1<<j] %= MOD;
                    }
                }
            }
        }
        int sum = 0;
        for (int i = 0; i <= 9; i++) {
            sum += dp[N][i][1023];
            sum %= MOD;
        }
        bw.write(sum + "\n");
        bw.close();
    }

}
```
