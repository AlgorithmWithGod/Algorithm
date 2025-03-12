```java
import java.io.*;
import java.util.*;
public class Main {

    static int N, M, D, maxEnemy;
    static int[][] original;
    static int[] archerCols;

    public static void main(String[] args) throws IOException {
        input();
        archerCols = new int[3];
        maxEnemy = 0;
        combination(0, 0);
        System.out.println(maxEnemy);
    }
    static void combination(int start, int idx) {
        if (idx == 3) {
            maxEnemy = Integer.max(maxEnemy, play());
            return;
        }
        for (int i = start; i < M; i++) {
            archerCols[idx] = i;
            combination(i + 1, idx + 1);
        }
    }

    static int play() {
        // 게임을 플레이 할 임시 격자판 생성
        int[][] board = new int[N][M];
        for (int i = 0; i < N; i++) {
            for (int j = 0 ; j < M; j++) {
                board[i][j] = original[i][j];
            }
        }
        int total = 0;
        do {
            total += shoot(board);
            moveEnemy(board);
        } while(!isEmpty(board));
        return total;
    }

    static void moveEnemy(int[][] board) {
        for (int r = N-2; r > -1; r--) {
            for (int c = 0; c < M; c++) {
                board[r+1][c] = board[r][c];
            }
        }
        // 맨 위 행은 0으로 채운다.
        Arrays.fill(board[0], 0);
    }
    static int shoot(int[][] board) {
        Set<Integer> killed = new HashSet<>();
        for (int archerCol : archerCols) {
            int minDist = D+1;
            int minLoc = -1;
            for (int r = 0; r < N; r++) {
                for (int c = 0; c < M; c++) {
                    if (board[r][c] == 0) continue;
                    int dist = getDist(N, archerCol, r, c);
                    if (dist <= D) {
                        if (dist < minDist || (dist == minDist && c < minLoc % M)) {
                            minDist = dist;
                            minLoc = r * M + c;
                        }
                    }
                }
            }
            if (minLoc == -1) { continue; }
            killed.add(minLoc);
        }

        // 제거한 적 위치 0으로 전환
        for (int k : killed) {
            int kr = k / M;
            int kc = k % M;
            board[kr][kc] = 0;
        }
        return killed.size();
    }

    static boolean isEmpty(int[][] board) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                if (board[i][j] == 1) { return false; }
            }
        }
        return true;
    }
    static int getDist(int r1, int c1, int r2, int c2) {
        return Math.abs(r1-r2) + Math.abs(c1-c2);
    }
    static void input() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        D = Integer.parseInt(st.nextToken());
        original = new int[N][M];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < M; j++) {
                original[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        br.close();
    }
}

```
