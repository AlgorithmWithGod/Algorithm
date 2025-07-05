```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int C = Integer.parseInt(st.nextToken());
        int N = Integer.parseInt(st.nextToken());
        
        int[] cost = new int[N];
        int[] customer = new int[N];
        
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            cost[i] = Integer.parseInt(st.nextToken());
            customer[i] = Integer.parseInt(st.nextToken());
        }
        
        int[] dp = new int[C + 101];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        
        for (int i = 0; i < N; i++) {
            for (int j = customer[i]; j < dp.length; j++) {
                if (dp[j - customer[i]] != Integer.MAX_VALUE) {
                    dp[j] = Math.min(dp[j], dp[j - customer[i]] + cost[i]);
                }
            }
        }
        
        int result = Integer.MAX_VALUE;
        for (int i = C; i < dp.length; i++) {
            result = Math.min(result, dp[i]);
        }
        
        System.out.println(result);
    }
}
```
