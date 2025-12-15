```java
import java.io.*;
import java.util.*;

public class Main {

    static int N, M;
    static boolean[][] map;
    static int answer = 0;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        map = new boolean[N][M];

        dfs(0, 0);

        System.out.println(answer);
    }

    static void dfs(int r, int c) {
        if (r == N) {
            answer++;
            return;
        }

        int nr = r;
        int nc = c + 1;
        if (nc == M) {
            nr = r + 1;
            nc = 0;
        }

        dfs(nr, nc);

        map[r][c] = true;

        if (!hasFull2x2()) {
            dfs(nr, nc);
        }

        map[r][c] = false;
    }

    static boolean hasFull2x2() {
        for (int i = 0; i < N - 1; i++) {
            for (int j = 0; j < M - 1; j++) {
                if (map[i][j] && map[i + 1][j] && map[i][j + 1] && map[i + 1][j + 1]) {
                    return true;
                }
            }
        }
        return false;
    }
}
```
