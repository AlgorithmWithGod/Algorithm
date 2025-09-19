```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) throws IOException {
        var br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int M = Integer.parseInt(br.readLine());
        boolean[] vip = new boolean[N + 1];

        for (int i = 0; i < M; i++) {
            int v = Integer.parseInt(br.readLine());
            vip[v] = true;
        }

        int[] dp = new int[N + 1];

        dp[0] = 1;
        dp[1] = 1;
        if (N >= 2) dp[2] = 2;
        for (int i = 3; i <= N; i++) {
            dp[i] = dp[i - 1] + dp[i - 2]; // 피보나치 쓰
        }

        int answer = 1;
        int prev = 0;
        for (int i = 1; i <= N; i++) {
            if (vip[i]) {
                int len = i - prev - 1;
                answer *= dp[len];
                prev = i;
            }
        }
        answer *= dp[N - prev];

        System.out.println(answer);
    }
}
```
