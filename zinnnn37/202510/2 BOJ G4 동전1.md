```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_2293_동전_1 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int N, K;
    private static int[] dp, coins;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        dp = new int[K + 1];
        coins = new int[N];
        for (int i = 0; i < N; i++) {
            coins[i] = Integer.parseInt(br.readLine());
        }
        dp[0] = 1;
    }

    private static void sol() throws IOException {
        for (int coin : coins) {
            for (int i = 1; i <= K; i++) {
                if (i - coin < 0) continue;

                dp[i] += dp[i - coin];
            }
        }
        bw.write(dp[K] + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```