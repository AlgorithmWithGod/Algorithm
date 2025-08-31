```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] block, dp;
    private static int N, sum;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        int answer = dp[0] > 0 ? dp[0] : -1;

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        sum = 0;

        block = new int[N];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            block[i] = Integer.parseInt(st.nextToken());
            sum += block[i];
        }

        dp = new int[sum + 1];
        Arrays.fill(dp, -1);
        dp[0] = 0;
    }

    private static void DP() {
        for (int i = 0; i < N; i++) {
            int[] newDp = dp.clone();

            for (int j = 0; j <= sum; j++) {
                if (dp[j] == -1) continue;

                int higher = dp[j];
                int lower = higher - j;

                newDp[j + block[i]] = Math.max(newDp[j + block[i]], higher + block[i]);

                int newLower = lower + block[i];
                if (newLower > higher) {
                    newDp[newLower - higher] = Math.max(newDp[newLower - higher], newLower);
                } else {
                    newDp[higher - newLower] = Math.max(newDp[higher - newLower], higher);
                }
            }

            dp = newDp;
        }
    }
}
```
