```java
import java.io.*;
import java.util.StringTokenizer;
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        final int N = Integer.parseInt(st.nextToken());
        final int M =Integer.parseInt(st.nextToken());
        final int K = Integer.parseInt(st.nextToken());

        int[] arr = new int[N];
        long[] dp = new long[N+1];
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }

        dp[1] = K;
        for (int index = 1; index < N; index++) {
            long min = Long.MAX_VALUE;
            long max = Long.MIN_VALUE;

            long finalMin = Long.MAX_VALUE;
            for (int i = 0; i < M; i++) {
                if(index - i - 1 < -1) break;
                min = Math.min(min, arr[index - i]);
                max = Math.max(max, arr[index - i]);
                finalMin = Math.min(finalMin, dp[index - i] + K + (i + 1) * (max - min));           
            }
        
            dp[index+1] = finalMin;
        }
        System.out.println(dp[N]);
        
    }
}
```
