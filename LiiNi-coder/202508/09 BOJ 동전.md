```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.StringTokenizer;

public class Main {
    private static BufferedReader br;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());
        StringTokenizer st;
        StringBuilder sb = new StringBuilder();
        
        for (int tc = 0; tc < T; tc++) {
            int n = Integer.parseInt(br.readLine());
            int[] coins = new int[n];
            st = new StringTokenizer(br.readLine());
            
            for (int i = 0; i < n; i++) {
                coins[i] = Integer.parseInt(st.nextToken());
            }
            int target = Integer.parseInt(br.readLine());
            int[] dp = new int[target + 1]; //dp[i] i원을 만드는 경우의수
            dp[0] = 1;
            for (int coin : coins) {
                for (int amount = coin; amount <= target; amount++) {
                    dp[amount] += dp[amount - coin];
                }
            }
            sb.append(dp[target]).append('\n');
        }
        System.out.print(sb.toString());
        br.close();
    }
}
```
