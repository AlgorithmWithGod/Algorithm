```java
import java.util.*;
import java.io.*;

public class boj6593 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static Pos start, end;
    static int L, R, C, answer;
    static char[][][] map;
    static int[][] dir = {{1,0,0}, {-1,0,0}, {0,1,0}, {0,-1,0}, {0,0,1}, {0,0,-1}};
    public static void main(String[] args) throws Exception {
        while (true) {
            nextLine();
            answer = Integer.MAX_VALUE;
            L = nextInt();
            R = nextInt();
            C = nextInt();
            if (L == 0 && R == 0 && C == 0) return;
            map = new char[L][R][C];
            for (int l = 0; l < L; l++) {
                for (int r = 0; r < R; r++) {
                    String str = br.readLine();
                    for (int c = 0; c < C; c++) {
                        map[l][r][c] = str.charAt(c);
                        if (map[l][r][c] == 'S') start = new Pos(l, r, c, 0);
                        else if (map[l][r][c] == 'E') end = new Pos(l, r, c, 0);
                    }
                }
                br.readLine();
            }
            bfs();
            if (answer != Integer.MAX_VALUE) System.out.println("Escaped in "+answer+" minute(s).");
            else System.out.println("Trapped!");
        }
    }

    static void bfs() {
        boolean[][][] visited = new boolean[L][R][C];
        Queue<Pos> q = new LinkedList<>();
        q.add(start);
        while (!q.isEmpty()) {
            Pos cur = q.poll();
            if ((cur.h == end.h) && (cur.r == end.r) && (cur.c == end.c)) {
                answer = Math.min(answer, cur.cnt);
                continue;
            }
            for (int[] d : dir) {
                int nh = cur.h + d[0];
                int nr = cur.r + d[1];
                int nc = cur.c + d[2];
                if (nh < 0 || nh >= L || nr < 0 || nr >= R || nc < 0 || nc >= C) continue;
                if (visited[nh][nr][nc] || map[nh][nr][nc] == '#') continue;
                q.add(new Pos(nh, nr, nc, cur.cnt+1));
                visited[nh][nr][nc] = true;
            }
        }
    }

    static class Pos {
        int h, r, c, cnt;
        public Pos(int h, int r, int c, int cnt) {
            this.h = h;
            this.r = r;
            this.c = c;
            this.cnt = cnt;
        }
    }
}
```
