```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_28423_게임 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int L, R, ans;
    private static int[]     memo;
    private static boolean[] checked;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        L = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());

        ans = 0;
        memo = new int[100_001];
        checked = new boolean[100_001];
        Arrays.fill(memo, 2);
    }

    private static void sol() throws IOException {
        for (int i = L; i <= R; i++) {
            ans += dfs(i);
        }
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static int dfs(int cur) {
        if (memo[cur] != 2) {
            return memo[cur];
        }

        if (checked[cur]) {
            return memo[cur] = 0;
        }

        checked[cur] = true;

        int A = 0;
        int B = 1;

        int tmp = cur;
        while (tmp != 0) {
            A += tmp % 10;
            B *= tmp % 10;
            tmp /= 10;
        }

        int res = Integer.parseInt(String.valueOf(A) + String.valueOf(B));

        if (cur == res) {
            memo[cur] = 1;
        } else if (res > 100000) {
            memo[cur] = -1;
        } else {
            memo[cur] = dfs(res);
        }
        checked[cur] = false;

        return memo[cur];
    }

}
```