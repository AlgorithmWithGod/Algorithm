```java
import java.io.*;
import java.util.*;

public class Main {
    static int n, m, h;
    static int[][][] box;
    static Queue<int[]> q = new LinkedList<>();

    static int[] dx = {-1, 1, 0, 0, 0, 0};
    static int[] dy = {0, 0, -1, 1, 0, 0};
    static int[] dz = {0, 0, 0, 0, -1, 1};

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        m = Integer.parseInt(st.nextToken());
        n = Integer.parseInt(st.nextToken());
        h = Integer.parseInt(st.nextToken());

        box = new int[h][n][m];

        int remain = 0;

        for (int z = 0; z < h; z++) {
            for (int x = 0; x < n; x++) {
                st = new StringTokenizer(br.readLine());
                for (int y = 0; y < m; y++) {
                    int v = Integer.parseInt(st.nextToken());
                    box[z][x][y] = v;

                    if (v == 1) q.offer(new int[]{z, x, y});
                    else if (v == 0) remain++;
                }
            }
        }

        if (remain == 0) {
            System.out.println(0);
            return;
        }

        int day = 0;

        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                int[] cur = q.poll();
                int cz = cur[0], cx = cur[1], cy = cur[2];

                for (int dir = 0; dir < 6; dir++) {
                    int nz = cz + dz[dir];
                    int nx = cx + dx[dir];
                    int ny = cy + dy[dir];

                    if (!isOk(nz, nx, ny)) continue;
                    if (box[nz][nx][ny] != 0) continue;

                    box[nz][nx][ny] = 1;
                    remain--;
                    q.offer(new int[]{nz, nx, ny});
                }
            }

            day++;

            if (remain == 0) {
                System.out.println(day);
                return;
            }
        }

        System.out.println(-1);
    }

    static boolean isOk(int z, int x, int y) {
        return !(z < 0 || z >= h || x < 0 || x >= n || y < 0 || y >= m);
    }
}

```
