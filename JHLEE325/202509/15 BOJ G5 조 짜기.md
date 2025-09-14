```java
import java.io.*;
import java.util.*;

public class Main {

    static List<Deque<Integer>> wheel = new ArrayList<>();

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];
        int[] dp = new int[n];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        for (int i = 0; i < n; i++) {
            int max = arr[i];
            int min = arr[i];
            for (int j = i; j >= 0; j--) {
                max = Math.max(max, arr[j]);
                min = Math.min(min, arr[j]);
                if (j == 0) {
                    dp[i] = Math.max(dp[i], max - min);
                } else {
                    dp[i] = Math.max(dp[i], dp[j - 1] + (max - min));
                }
            }
        }

        System.out.println(dp[n - 1]);
    }
}
```
