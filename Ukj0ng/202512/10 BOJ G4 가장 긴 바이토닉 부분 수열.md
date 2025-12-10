```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr, dp, dp1, dp2;
    private static int N, answer;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        StringTokenizer st = new StringTokenizer(br.readLine());
        arr = new int[N];
        dp = new int[N];
        dp1 = new int[N];
        dp2 = new int[N];

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.fill(dp1, 1);
        Arrays.fill(dp2, 1);
    }

    private static void DP() {
        for (int i = 1; i < N; i++) {
            for (int j = 0; j < i; j++) {
                if (arr[i] > arr[j]) {
                    dp1[i] = Math.max(dp1[i], dp1[j]+1);
                }
            }
        }

        for (int i = N-2; i >= 0; i--) {
            for (int j = N-1; j > i; j--) {
                if (arr[i] > arr[j]) {
                    dp2[i] = Math.max(dp2[i], dp2[j]+1);
                }
            }
        }

        for (int i = 0; i < N; i++) {
            dp[i] = dp1[i] + dp2[i] - 1;
            answer = Math.max(answer, dp[i]);
        }
    }
}
```
