```java
import java.io.*;
import java.util.*;

public class Main {
    static int N, M, H, answer;
    static int[][] map;
    static boolean finish = false;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        H = Integer.parseInt(st.nextToken());

        map = new int[H + 1][N + 1];

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            map[a][b] = 1;
        }

        for (int i = 0; i <= 3; i++) {
            answer = i;
            dfs(1, 0);
            if (finish) break;
        }

        System.out.println(finish ? answer : -1);
    }

    static void dfs(int startR, int count) {
        if (finish) return;
        if (answer == count) {
            if (check()) finish = true;
            return;
        }

        for (int i = startR; i <= H; i++) {
            for (int j = 1; j < N; j++) {
                if (map[i][j] == 1) continue;
                if (map[i][j - 1] == 1) continue;
                if (j + 1 <= N && map[i][j + 1] == 1) continue;

                map[i][j] = 1;
                dfs(i, count + 1);
                map[i][j] = 0;
            }
        }
    }

    static boolean check() {
        for (int i = 1; i <= N; i++) {
            int currentPos = i;
            for (int j = 1; j <= H; j++) {
                if (map[j][currentPos] == 1) {
                    currentPos++;
                } else if (map[j][currentPos - 1] == 1) {
                    currentPos--;
                }
            }
            if (currentPos != i) return false;
        }
        return true;
    }
}
```
