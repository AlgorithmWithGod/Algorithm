```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int[] arr = new int[N + 1];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for(int i = 1; i <= N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        int[] dp = new int[N + 1];
        dp[0] = 0;

        for(int i = 1; i <= N; i++) {
            dp[i] = 0;
            int mx = arr[i];
            int mn = arr[i];
            for(int j = i; j >= 1; j--) {
                mx = Math.max(mx, arr[j]);
                mn = Math.min(mn, arr[j]);
                dp[i] = Math.max(dp[i], dp[j-1] + (mx-mn));
            }
        }

        System.out.println(dp[N]);
    }
}

```
