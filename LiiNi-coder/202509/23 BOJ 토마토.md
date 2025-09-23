```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int m = Integer.parseInt(st.nextToken());
        int n = Integer.parseInt(st.nextToken());
        int h = Integer.parseInt(st.nextToken());
        int[][][] box = new int[h][n][m];
        Queue<int[]> q = new ArrayDeque<>();


        for (int k = 0; k < h; k++) {
            for (int i = 0; i < n; i++) {
                st = new StringTokenizer(br.readLine());
                for (int j = 0; j < m; j++) {
                    box[k][i][j] = Integer.parseInt(st.nextToken());
                    if (box[k][i][j] == 1) {
                        q.add(new int[]{k, i, j});
                    }
                }
            }
        }

        int[] dz = {0, 0, 0, 0, 1, -1};
        int[] dx = {1, -1, 0, 0, 0, 0};
        int[] dy = {0, 0, 1, -1, 0, 0};
        int days = -1;
        while (!q.isEmpty()) {
            int size = q.size();
            for (int s = 0; s < size; s++) {
                int[] cur = q.poll();
                int z = cur[0], x = cur[1], y = cur[2];
                for (int d = 0; d < 6; d++) {
                    int nz = z + dz[d], nx = x + dx[d], ny = y + dy[d];
                    if (nz < 0 ||nz >= h|| nx < 0 || nx >= n || ny < 0 || ny >= m)
                        continue;
                    if (box[nz][nx][ny] == 0) {
                        box[nz][nx][ny] = 1;
                        q.add(new int[]{nz, nx, ny});
                    }
                }
            }
            days++;
        }

        for (int z = 0; z < h; z++) {
            for (int x = 0; x < n; x++) {
                for (int y = 0; y < m; y++) {
                    if (box[z][x][y] == 0) {
                        System.out.println(-1);
                        return;
                    }
                }
            }
        }
        System.out.println(days);
    }
}

```
