```java
import java.io.*;
import java.util.*;

public class Main {

    static int[][] map;
    static int w, h;
    static Queue<int[]> fireQ;
    static Queue<int[]> humanQ;
    static StringBuilder sb = new StringBuilder();
    static int[] dr = {-1, 1, 0, 0};
    static int[] dc = {0, 0, -1, 1};
    static boolean[][] fireVisited;
    static boolean[][] humanVisited;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            st = new StringTokenizer(br.readLine());
            w = Integer.parseInt(st.nextToken());
            h = Integer.parseInt(st.nextToken());

            map = new int[h][w];
            fireVisited = new boolean[h][w];
            humanVisited = new boolean[h][w];

            fireQ = new ArrayDeque<>();
            humanQ = new ArrayDeque<>();

            int sr = -1, sc = -1;

            for (int i = 0; i < h; i++) {
                String str = br.readLine();
                for (int j = 0; j < w; j++) {
                    char ch = str.charAt(j);
                    if (ch == '#') {
                        map[i][j] = 1;
                    } else {
                        map[i][j] = 0;
                        if (ch == '@') {
                            humanQ.add(new int[]{i, j});
                            humanVisited[i][j] = true;
                            sr = i; sc = j;
                        } else if (ch == '*') {
                            fireQ.add(new int[]{i, j});
                            fireVisited[i][j] = true;
                        }
                    }
                }
            }

            if (sr == 0 || sr == h - 1 || sc == 0 || sc == w - 1) {
                sb.append("1\n");
            } else {
                bfs();
            }
        }
        System.out.print(sb.toString());
    }

    public static void bfs() {
        int time = 1;

        while (!humanQ.isEmpty()) {
            int fs = fireQ.size();
            for (int i = 0; i < fs; i++) {
                int[] cur = fireQ.poll();
                for (int d = 0; d < 4; d++) {
                    int nr = cur[0] + dr[d];
                    int nc = cur[1] + dc[d];
                    if (nr < 0 || nr >= h || nc < 0 || nc >= w) continue;
                    if (map[nr][nc] == 1 || fireVisited[nr][nc]) continue;
                    fireVisited[nr][nc] = true;
                    fireQ.add(new int[]{nr, nc});
                }
            }

            int hs = humanQ.size();
            for (int i = 0; i < hs; i++) {
                int[] cur = humanQ.poll();

                if (cur[0] == 0 || cur[0] == h - 1 || cur[1] == 0 || cur[1] == w - 1) {
                    sb.append(time).append('\n');
                    humanQ.clear();
                    fireQ.clear();
                    return;
                }

                for (int d = 0; d < 4; d++) {
                    int nr = cur[0] + dr[d];
                    int nc = cur[1] + dc[d];
                    if (nr < 0 || nr >= h || nc < 0 || nc >= w) continue;
                    if (map[nr][nc] == 1) continue;
                    if (humanVisited[nr][nc]) continue;
                    if (fireVisited[nr][nc]) continue;
                    humanVisited[nr][nc] = true;
                    humanQ.add(new int[]{nr, nc});
                }
            }
            time++;
        }

        sb.append("IMPOSSIBLE\n");
    }
}

```
