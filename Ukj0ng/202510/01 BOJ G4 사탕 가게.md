```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] dp, w, v;
    private static int N, m;
    private static double M;
    public static void main(String[] args) throws IOException {

        while (true) {
            init();
            if (N == 0 && M == 0.0) break;

            DP();
            int answer = 0;
            for (int i = 0; i <= m; i++) {
                answer = Math.max(answer, dp[i]);
            }

            bw.write(answer + "\n");
        }

        bw.write("\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Double.parseDouble(st.nextToken()) * 100;

        if (N == 0 && M == 0.0) return;
        m = (int) (M+0.5);

        w = new int[N];
        v = new int[N];

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            v[i] = Integer.parseInt(st.nextToken());
            w[i] = (int) (Double.parseDouble(st.nextToken()) * 100 + 0.5);
        }

        dp = new int[m+1];
    }

    private static void DP() {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j <= m; j++) {
                if (j - w[i] >= 0) {
                    dp[j] = Math.max(dp[j], dp[j - w[i]] + v[i]);
                }
            }
        }
    }
}
```
