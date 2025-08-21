```java
import java.io.*;
import java.util.*;

public class Main {

    static int[] dr = {-1, -1, 0, 1, 1, 1, 0, -1};
    static int[] dc = { 0, -1,-1,-1, 0, 1, 1,  1};

    static class fish {
        int r, c, dir;
        boolean live;

        public fish(int row, int col, int d) {
            this.r = row;
            this.c = col;
            this.dir = d;
            this.live = true;
        }
    }

    static class shark {
        int r, c, eat, dir;

        public shark(int row, int col, int e, int d) {
            this.r = row;
            this.c = col;
            this.eat = e;
            this.dir = d;
        }
    }

    static int[][] map = new int[4][4];
    static fish[] list = new fish[17];
    static int answer = 0;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        shark s = null;

        for (int i = 0; i < 4; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 4; j++) {
                int n = Integer.parseInt(st.nextToken());
                int d = Integer.parseInt(st.nextToken()) - 1;
                map[i][j] = n;
                list[n] = new fish(i, j, d);
            }
        }

        int first = map[0][0];
        fish f0 = list[first];
        f0.live = false;
        s = new shark(0, 0, first, f0.dir);
        map[0][0] = 0;

        dfs(copymap(map), copylist(list), s);

        System.out.println(answer);
    }

    static void dfs(int[][] curmap, fish[] curlist, shark s) {
        answer = Math.max(answer, s.eat);

        moveFish(curmap, curlist, s);

        int sr = s.r, sc = s.c, dir = s.dir;
        for (int step = 1; step <= 3; step++) {
            int nr = sr + dr[dir] * step;
            int nc = sc + dc[dir] * step;

            if (nr < 0 || nr >= 4 || nc < 0 || nc >= 4) break;
            if (curmap[nr][nc] == 0) continue;

            int[][] nMap = copymap(curmap);
            fish[] nList = copylist(curlist);

            int target = nMap[nr][nc];
            fish eaten = nList[target];
            eaten.live = false;

            shark ns = new shark(nr, nc, s.eat + target, eaten.dir);

            nMap[sr][sc] = 0;
            nMap[nr][nc] = 0;

            dfs(nMap, nList, ns);
        }
    }

    static void moveFish(int[][] curmap, fish[] curlist, shark s) {
        for (int i = 1; i <= 16; i++) {
            fish f = curlist[i];
            if (f == null || !f.live) continue;

            for (int rotate = 0; rotate < 8; rotate++) {
                int nd = (f.dir + rotate) % 8;
                int nr = f.r + dr[nd];
                int nc = f.c + dc[nd];

                if (nr < 0 || nr >= 4 || nc < 0 || nc >= 4) continue;
                if (nr == s.r && nc == s.c) continue;

                if (curmap[nr][nc] == 0) {
                    curmap[f.r][f.c] = 0;
                    f.r = nr; f.c = nc; f.dir = nd;
                    curmap[nr][nc] = i;
                } else {
                    int otherNum = curmap[nr][nc];
                    fish g = curlist[otherNum];

                    curmap[f.r][f.c] = otherNum;
                    curmap[nr][nc] = i;

                    int tr = f.r, tc = f.c;
                    f.r = nr; f.c = nc; f.dir = nd;
                    g.r = tr; g.c = tc;
                }
                break;
            }
        }
    }

    static int[][] copymap(int[][] src) {
        int[][] cpymap = new int[4][4];
        for (int i = 0; i < 4; i++) {
            System.arraycopy(src[i], 0, cpymap[i], 0, 4);
        }
        return cpymap;
    }

    static fish[] copylist(fish[] src) {
        fish[] cpylist = new fish[17];
        for (int i = 1; i <= 16; i++) {
            if (src[i] == null) continue;
            fish f = src[i];
            fish nf = new fish(f.r, f.c, f.dir);
            nf.live = f.live;
            cpylist[i] = nf;
        }
        return cpylist;
    }
}

```
