```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] dp;
    private static int n, t;

    public static void main(String[] args) throws IOException {
        init();
        solve();
        
        bw.write(dp[t] + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        t = Integer.parseInt(st.nextToken());
        dp = new int[t + 1];
    }

    private static void solve() throws IOException {
        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int k = Integer.parseInt(st.nextToken());
            int s = Integer.parseInt(st.nextToken());
            
            for (int j = t; j >= k; j--) {
                dp[j] = Math.max(dp[j], dp[j - k] + s);
            }
        }
    }
}
```
