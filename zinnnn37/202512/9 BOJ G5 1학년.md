```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int      N;
    private static int[]    nums;
    private static long[][] dp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        nums = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            nums[i] = Integer.parseInt(st.nextToken());
        }
        dp = new long[N][21];
        dp[0][nums[0]] = 1;
    }

    private static void sol() throws IOException {
        for (int i = 1; i < N - 1; i++) {
            for (int prev = 0; prev <= 20; prev++) {
                if (dp[i - 1][prev] == 0) continue;

                int sum = prev + nums[i];
                int gap = prev - nums[i];

                if (sum <= 20) {
                    dp[i][sum] += dp[i - 1][prev];
                }
                if (gap >= 0) {
                    dp[i][gap] += dp[i - 1][prev];
                }
            }
        }
        bw.write(dp[N - 2][nums[N - 1]] + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```