```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_14846_직사각형과_쿼리 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder sb = new StringBuilder();
    private static StringTokenizer st;

    private static int N, Q, ans;
    private static int[][] nums;
    private static int[][][] prefix;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        nums = new int[N + 1][N + 1];
        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                nums[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        prefix = new int[N + 1][N + 1][11];
        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++) {
                for (int a = 0; a <= 10; a++) {
                    prefix[i][j][a] += prefix[i - 1][j][a];
                    prefix[i][j][a] += prefix[i][j - 1][a];
                    prefix[i][j][a] -= prefix[i - 1][j - 1][a];
                }
                prefix[i][j][nums[i][j]]++;
            }
        }
        Q = Integer.parseInt(br.readLine());
    }

    private static void sol() throws IOException {
        while (Q-- > 0) {
            st = new StringTokenizer(br.readLine());

            int x1 = Integer.parseInt(st.nextToken()) - 1;
            int y1 = Integer.parseInt(st.nextToken()) - 1;
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());

            ans = 0;
            for (int k = 1; k <= 10; k++) {
                int count = prefix[x2][y2][k] - prefix[x1][y2][k]
                        - prefix[x2][y1][k] + prefix[x1][y1][k];
                if (count > 0) ans++;
            }
            sb.append(ans).append("\n");
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

}
```