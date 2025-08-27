```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static TreeSet<Integer>[] dp;
    private static int[] arr;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();
        DP();

        bw.write(dp[M].last() + "\n");

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        arr = new int[N + 1];
        dp = new TreeSet[M + 1];

        for (int i = 0; i <= M; i++) {
            dp[i] = new TreeSet<>();
        }

        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            arr[i] = Math.abs(Integer.parseInt(st.nextToken()));
        }
    }

    private static void DP() {
        dp[0].add(0);
        for (int i = 1; i <= M; i++) {
            for (int j = 1; j <= N; j++) {
                for (int val : dp[i - 1]) {
                    dp[i].add(arr[j] ^ val);
                }
            }
        }
    }
}

```
