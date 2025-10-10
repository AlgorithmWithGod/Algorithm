```java
package etc;

import java.io.*;
import java.util.StringTokenizer;

public class BJ_1034_램프 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int N, M, K, max;
    private static boolean[][] lamp;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        lamp = new boolean[N][M];
        for (int i = 0; i < N; i++) {
            String s = br.readLine();
            for (int j = 0; j < M; j++) {
                lamp[i][j] = s.charAt(j) == '1';
            }
        }

        K = Integer.parseInt(br.readLine());
        max = 0;
    }

    private static void sol() throws IOException {
        for (int i = 0; i < N; i++) {
            int toTurnOn = 0;

            for (int j = 0; j < M; j++) {
                if (!lamp[i][j]) toTurnOn++;
            }

            // (K - 켜야 하는 열의 수)가 홀수면 켜지 않아야 할 다른 열도 켜지기 때문에 걸러야 함
            if (toTurnOn > K || (K - toTurnOn) % 2 != 0) continue;

            // 행 개수 세기
            int cnt = 0;
            for (int k = 0; k < N; k++) {
                if (isAllTurnedOn(i, k)) cnt++;
            }
            max = Math.max(max, cnt);
        }
        bw.write(max + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static boolean isAllTurnedOn(int row1, int row2) {
        for (int j = 0; j < M; j++) {
            if (lamp[row1][j] != lamp[row2][j]) return false;
        }
        return true;
    }

}
```