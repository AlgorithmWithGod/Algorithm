```java
import java.io.*;
import java.util.*;

public class Main {

    static class Shark {
        int r, c, s, d, z;
        boolean alive;

        Shark(int r, int c, int s, int d, int z) {
            this.r = r; this.c = c; this.s = s; this.d = d; this.z = z;
            this.alive = true;
        }
    }

    static int R, C, M;
    static Shark[] sharks;
    static int[][] board;
    static final int[] dr = {0, -1, 1, 0, 0};
    static final int[] dc = {0, 0, 0, 1, -1};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        st = new StringTokenizer(br.readLine());
        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        sharks = new Shark[M];
        board = new int[R + 1][C + 1];
        for (int i = 1; i <= R; i++) Arrays.fill(board[i], -1);

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int r = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            int s = Integer.parseInt(st.nextToken());
            int d = Integer.parseInt(st.nextToken());
            int z = Integer.parseInt(st.nextToken());
            sharks[i] = new Shark(r, c, s, d, z);
        }

        for (int i = 0; i < M; i++) {
            if (sharks[i].alive) board[sharks[i].r][sharks[i].c] = i;
        }

        int answer = 0;

        for (int col = 1; col <= C; col++) {
            for (int row = 1; row <= R; row++) {
                int idx = board[row][col];
                if (idx != -1 && sharks[idx].alive) {
                    sharks[idx].alive = false;
                    answer += sharks[idx].z;
                    board[row][col] = -1;
                    break;
                }
            }

            moveAll();

            resolveConflicts();
        }

        System.out.println(answer);
    }

    static void moveAll() {
        for (int i = 1; i <= R; i++) Arrays.fill(board[i], -1);

        for (int i = 0; i < M; i++) {
            Shark s = sharks[i];
            if (!s.alive) continue;

            int nr = s.r, nc = s.c, nd = s.d, rem = s.s;
            while (rem-- > 0) {
                int tr = nr + dr[nd];
                int tc = nc + dc[nd];

                if (tr < 1 || tr > R || tc < 1 || tc > C) {
                    if (nd == 1) nd = 2;
                    else if (nd == 2) nd = 1;
                    else if (nd == 3) nd = 4;
                    else nd = 3;
                    tr = nr + dr[nd];
                    tc = nc + dc[nd];
                }

                nr = tr; nc = tc;
            }

            s.r = nr; s.c = nc; s.d = nd;

            if (board[nr][nc] == -1) board[nr][nc] = i;
            else {
                board[nr][nc] = -2;
            }
        }
    }

    static void resolveConflicts() {
        int[][] newBoard = new int[R + 1][C + 1];
        for (int i = 1; i <= R; i++) Arrays.fill(newBoard[i], -1);

        for (int i = 0; i < M; i++) {
            Shark s = sharks[i];
            if (!s.alive) continue;
            int r = s.r, c = s.c;

            int curIdx = newBoard[r][c];
            if (curIdx == -1) {
                newBoard[r][c] = i;
            } else {
                if (sharks[curIdx].z < s.z) {
                    sharks[curIdx].alive = false;
                    newBoard[r][c] = i;
                } else {
                    s.alive = false;
                }
            }
        }

        board = newBoard;
    }
}

```
