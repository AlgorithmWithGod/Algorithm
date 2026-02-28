```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_16987_계란으로_계란치기 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, ans;
    private static int[][] eggs;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        eggs = new int[N][2];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());

            eggs[i][0] = Integer.parseInt(st.nextToken());
            eggs[i][1] = Integer.parseInt(st.nextToken());
        }
    }

    private static void sol() throws IOException {
        dfs(0, 0);

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void dfs(int depth, int broken) {
        if (depth == N) {
            ans = Math.max(ans, broken);
            return;
        }

        if (eggs[depth][0] <= 0) {
            dfs(depth + 1, broken);
            return;
        }

        boolean canHit = false;

        for (int i = 0; i < N; i++) {
            if (i == depth) continue;
            if (eggs[i][0] <= 0) continue;

            canHit = true;

            int beforeCur = eggs[depth][0];
            int beforeOp  = eggs[i][0];

            eggs[depth][0] -= eggs[i][1];
            eggs[i][0] -= eggs[depth][1];

            int brokenNow = 0;
            if (beforeCur > 0 && eggs[depth][0] <= 0) brokenNow++;
            if (beforeOp > 0 && eggs[i][0] <= 0) brokenNow++;

            dfs(depth + 1, broken + brokenNow);

            eggs[depth][0] = beforeCur;
            eggs[i][0] = beforeOp;
        }

        if (!canHit) {
            dfs(depth + 1, broken);
        }
    }

}
```