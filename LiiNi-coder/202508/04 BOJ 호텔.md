```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {

    static int C, N;
    static int[] cost, customer;
    static int[] dp;
    static final int INF = 100000;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        C = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());
        cost = new int[N];
        customer = new int[N];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            cost[i] = Integer.parseInt(st.nextToken());
            customer[i] = Integer.parseInt(st.nextToken());
        }

        dp = new int[INF];
        for (int i = 0; i < INF; i++) {
            dp[i] = 0;
        }

        for (int i = 0; i < N; i++) {
            for (int j = cost[i]; j < INF; j++) {
                dp[j] = Math.max(dp[j], dp[j - cost[i]] + customer[i]);
            }
        }
        int answer = Integer.MAX_VALUE;
        for (int i = 0; i < INF; i++) {
            if (dp[i] >= C) {
                answer = i;
                break;
            }
        }
        System.out.println(answer);
    }
}
```
