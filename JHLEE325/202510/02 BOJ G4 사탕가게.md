```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        while (true) {
            st = new StringTokenizer(br.readLine());

            int n = Integer.parseInt(st.nextToken());
            int m = (int) (Double.parseDouble(st.nextToken()) * 100.0 + 0.5);

            if (n == 0 && m == 0) {
                break;
            }

            int[] dp = new int[m + 1];

            int[] cal = new int[n];
            int[] price = new int[n];

            for (int i = 0; i < n; i++) {
                st = new StringTokenizer(br.readLine());
                cal[i] = Integer.parseInt(st.nextToken());
                price[i] = (int) (Double.parseDouble(st.nextToken()) * 100.0 + 0.5);
            }

            for (int i = 1; i <= m; i++) {
                for (int j = 0; j < n; j++) {
                    if (i >= price[j]) {
                        dp[i] = Math.max(dp[i], dp[i - price[j]] + cal[j]);
                    }
                }
            }

            System.out.println(dp[m]);
        }
    }
}```
