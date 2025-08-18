```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    private static BufferedReader br;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine().trim());

        StringBuilder sb = new StringBuilder();
        for (int tc = 0; tc < T; tc++) {
            int N = Integer.parseInt(br.readLine().trim());
            int[] coins = new int[N];
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int i = 0; i < N; i++) {
                coins[i] = Integer.parseInt(st.nextToken());
            }
            int target = Integer.parseInt(br.readLine().trim());
            int[] dp = new int[target + 1];
            dp[0] = 1;

            for (int coin : coins) {
                for (int amt = coin; amt <= target; amt++) {
                    dp[amt] += dp[amt - coin];
                }
            }

            sb.append(dp[target]).append('\n');
        }

        System.out.print(sb.toString());
        br.close();
    }
```
