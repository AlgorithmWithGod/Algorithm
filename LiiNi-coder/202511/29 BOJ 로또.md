```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int T = Integer.parseInt(st.nextToken());
        while(T-- > 0){
            st = new StringTokenizer(br.readLine());
            int n = Integer.parseInt(st.nextToken());
            int m = Integer.parseInt(st.nextToken());
            long[][] dp = new long[n + 1][m + 1];
            for(int j = 1; j <= m; j++){
                dp[1][j] = 1;
            }

            for(int k = 2; k <= n; k++){
                for(int j = 1; j <= m; j++){
                    long sum = 0;
                    for(int prev = 1; prev * 2 <= j; prev++){
                        sum += dp[k-1][prev];
                    }
                    dp[k][j] = sum;
                }
            }
            long answer = 0;
            
            
            for(int j = 1; j <= m; j++){
                answer += dp[n][j];
            }
            System.out.println(answer);
        }
    }
}

```
