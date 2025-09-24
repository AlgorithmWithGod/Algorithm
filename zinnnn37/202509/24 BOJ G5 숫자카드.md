```java
package etc;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class BJ_2591_숫자카드 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    private static int len;
    private static String input;
    private static int[] nums;
    private static int[] dp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        input = br.readLine();
        len = input.length();

        nums = new int[len + 1];
        dp = new int[len + 1];
        for (int i = 1; i <= len; i++) {
            nums[i] = input.charAt(i - 1) - '0';
        }
        dp[0] = 1;
    }

    private static void sol() throws IOException {
        for (int i = 1; i <= len; i++) {
            if (nums[i] > 0) {
                dp[i] = dp[i - 1];
            }

            if (i >= 2 && nums[i - 1] != 0 && nums[i - 1] * 10 + nums[i] <= 34) {
                dp[i] += dp[i - 2];
            }
        }
        bw.write(dp[len] + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```