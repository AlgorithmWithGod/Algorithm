```java
import java.util.*;

class Solution {
    int[] Dr = {-1, 1, 0, 0};
    int[] Dc = {0, 0, -1, 1};
    int Rr, Rc, Gr, Gc;
    int H;
    int W;
    boolean[][] visited;

    public int solution(String[] board) {

        H = board.length;
        W = board[0].length();
        visited = new boolean[H][W];

        for (int i = 0; i < H; i++) {
            for (int j = 0; j < W; j++) {
                char c = board[i].charAt(j);
                if (c == 'R') {
                    Rr = i;
                    Rc = j;
                }
                if (c == 'G') {
                    Gr = i;
                    Gc = j;
                }
            }
        }
        Queue<int[]> q = new ArrayDeque<>();
        q.add(new int[]{Rr, Rc, 0});
        visited[Rr][Rc] = true;

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int r = cur[0];
            int c = cur[1];
            int d = cur[2];
            if (r == Gr && c == Gc) {
                return d;
            }
            for (int i = 0; i < 4; i++) {
                int[] next = slide(r, c, i, board);
                int nr = next[0], nc = next[1];
                if (visited[nr][nc])
                    continue;
                
                visited[nr][nc] = true;
                q.add(new int[]{nr, nc, d + 1});
            }
        }
        
        return -1;
    }

    int[] slide(int r, int c, int direction, String[] board) {
        int nr = r, nc = c;
        while (true) {
            int tr = nr + Dr[direction];
            int tc = nc + Dc[direction];
            if (tr < 0 || tr >= H || tc < 0 || tc >= W)
                break;
            if (board[tr].charAt(tc) == 'D')
                break;
            nr = tr;
            nc = tc;
        }
        return new int[]{nr, nc};
    }
}

```
