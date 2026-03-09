```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        int[] dp = new int[N + 1];
        int res = 0;

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            int time = Integer.parseInt(st.nextToken());
            int count = Integer.parseInt(st.nextToken());

            int prevTask = 0;
            for (int j = 0; j < count; j++) {
                int prev = Integer.parseInt(st.nextToken());
                prevTask = Math.max(prevTask, dp[prev]);
            }

            dp[i] = prevTask + time;

            res = Math.max(res, dp[i]);
        }

        System.out.println(res);
    }
}
```
