```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    private static BufferedReader br;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int[] Arr = new int[N + 1];
        StringTokenizer st = new StringTokenizer(br.readLine());


        for (int i = 1; i <= N; i++) {
            Arr[i] = Integer.parseInt(st.nextToken());
        }

        int[] dp = new int[N + 1];
        dp[0] = 0;
        for (int i = 1; i <= N; i++) {
            int max = Arr[i];
            int min = Arr[i];
            dp[i] = Integer.MAX_VALUE;
            for (int j = i; j >= 1; j--) {
                max = Math.max(max, Arr[j]);
                min = Math.min(min, Arr[j]);
                dp[i] = Math.min(dp[i], dp[j - 1] + (max - min));
            }
        }

        System.out.println(dp[N]);
    }
}
```
