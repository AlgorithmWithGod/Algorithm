```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_18808_스티커_붙이기 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M, K, R, C, ans;
    private static int[][] laptop, sticker, rotated;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        laptop = new int[N][M];
    }

    private static void sol() throws IOException {
        while (K-- > 0) {
            st = new StringTokenizer(br.readLine());
            R = Integer.parseInt(st.nextToken());
            C = Integer.parseInt(st.nextToken());

            sticker = new int[R][C];
            for (int i = 0; i < R; i++) {
                st = new StringTokenizer(br.readLine());
                for (int j = 0; j < C; j++) {
                    sticker[i][j] = Integer.parseInt(st.nextToken());
                }
            }

            for (int dir = 0; dir < 4; dir++) {
                if (attach()) {
                    break;
                }
                rotate(dir);
            }
        }
        printAns();
    }

    private static boolean attach() {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                // 스티커가 노트북 범위를 벗어남
                if (i + R - 1 >= N || j + C - 1 >= M) continue;

                // sticker attached
                if (checkValid(i, j)) return true;
            }
        }
        return false;
    }

    private static boolean checkValid(int x, int y) {
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                // attachment unavailable
                if (laptop[x + i][y + j] == 1 && sticker[i][j] == 1) return false;
            }
        }

        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                if (sticker[i][j] == 0) continue;

                laptop[x + i][y + j] = 1;
            }
        }
        return true;
    }

    private static void rotate(int dir) {
        int nR = C;
        int nC = R;

        rotated = new int[nR][nC];
        for (int i = 0; i < nR; i++) {
            for (int j = 0; j < nC; j++) {
                rotated[i][j] = sticker[R - j - 1][i];
            }
        }
        R = nR;
        C = nC;
        sticker = rotated;
    }

    private static void printAns() throws IOException {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (laptop[i][j] == 1) ans++;
            }
        }
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```