```
import java.io.*;
import java.util.HashSet;
import java.util.Set;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Set<Integer>[] dp;
    private static int[] weight;
    private static int N, sum, max;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        int answer = 0;

        for (int val : dp[dp.length-1]) {
            answer = Math.max(val, answer);
        }

        if (N%2 == 1) {
            for (int val : dp[dp.length-2]) {
                answer = Math.max(val, answer);
            }
        }

        bw.write(answer + " " + (sum - answer) + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        sum = 0;
        max = 0;

        int length = N/2;
        if (N%2 == 1) length++;
        weight = new int[N];
        dp = new Set[length + 1];
        for (int i = 0; i < dp.length; i++) {
            dp[i] = new HashSet<>();
        }

        dp[0].add(0);

        for (int i = 0; i < N; i++) {
            weight[i] = Integer.parseInt(br.readLine());
            sum += weight[i];
        }

        max = sum / 2;
    }

    private static void DP() {
        for (int i = 0; i < N; i++) {
            for (int j = dp.length-1; j > 0; j--) {
                if (!dp[j-1].isEmpty()) {
                    for (int val : dp[j-1]) {
                        int result = val + weight[i];
                        if (result <= max) {
                            dp[j].add(result);
                        }
                    }
                }
            }
        }
    }
}
```
