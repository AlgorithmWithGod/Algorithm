```java
import java.io.*;
import java.util.*;

public class Main {
    private static final int MOD = 1_000_000_000;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());

        int[][] dp = new int[N + 1][K + 1];

        for(int j = 1; j <= K; j++){
            dp[0][j] = 1;
        }
        for(int i = 0; i <= N; i++){
            dp[i][1] = 1;
        }

        
        for(int i = 1; i <= N; i++){
            for(int j = 2; j <= K; j++){
                dp[i][j] = (dp[i][j - 1] + dp[i - 1][j]) % MOD;
            }
        }
        System.out.println(dp[N][K]);
    }
}

```
