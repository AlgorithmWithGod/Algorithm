```java
import java.io.*;
import java.util.StringTokenizer;

public class Main {
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};

    static int R, C;
    static int[][] map;
    static int answer = Integer.MIN_VALUE;
    
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        map = new int[R][C];

        for (int i = 0; i < R; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < C; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                dfs(0, map[i][j], i, j, 0);
            }
        }

        System.out.println(answer);
    }

    private static void dfs(int length, int sum, int x, int y, int direction) {
        if (length == 3) {
            answer = Math.max(answer, sum);
            return;
        }

        if (length == 1) {
            // ㅗ 모양 처리
            if (direction == 0 || direction == 1) {  // 위/아래로 움직인 경우
                int nx1 = x + dx[2];
                int ny1 = y + dy[2];
                int nx2 = x + dx[3];
                int ny2 = y + dy[3];
                if (!cannotMove(nx1, ny1) && !cannotMove(nx2, ny2)) {
                    answer = Math.max(answer, sum + map[nx1][ny1] + map[nx2][ny2]);
                }
            } else if (direction == 2 || direction == 3) {  // 좌/우로 움직인 경우
                int nx1 = x + dx[0];
                int ny1 = y + dy[0];
                int nx2 = x + dx[1];
                int ny2 = y + dy[1];
                if (!cannotMove(nx1, ny1) && !cannotMove(nx2, ny2)) {
                    answer = Math.max(answer, sum + map[nx1][ny1] + map[nx2][ny2]);
                }
            }
        }

        for (int i = 0; i < 4; i++) {
            if (length != 0) {
                if (i == 0 && direction == 1) continue;
                if (i == 1 && direction == 0) continue;
                if (i == 2 && direction == 3) continue;
                if (i == 3 && direction == 2) continue;
            }
            int nx = x + dx[i];
            int ny = y + dy[i];
            if (cannotMove(nx, ny) ) continue;

            dfs(length + 1, sum + map[nx][ny], nx, ny, i);
        }
    }

    private static boolean cannotMove(int nx, int ny) {
        return (nx < 0 || ny < 0 || nx >= R || ny >= C);
    }
}
```
