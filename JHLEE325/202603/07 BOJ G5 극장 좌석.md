```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        
        int N = Integer.parseInt(br.readLine());
        int M = Integer.parseInt(br.readLine());

        int[] dp = new int[41];
        dp[0] = 1;
        dp[1] = 1;
        for (int i = 2; i <= 40; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        int answer = 1;
        int vipNum = 0;

        for (int i = 0; i < M; i++) {
            int vip = Integer.parseInt(br.readLine());
            int vipDist = vip - vipNum - 1;
            answer *= dp[vipDist];
            vipNum = vip;
        }

        answer *= dp[N - vipNum];

        System.out.println(answer);
    }
}
```
