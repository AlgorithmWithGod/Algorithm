```java
import java.io.*;
import java.util.*;

public class Main {

    static char[][] map = new char[5][5];
    static int[] selected = new int[7];
    static int ans = 0;
    static int[] dr = {-1, 1, 0, 0};
    static int[] dc = {0, 0, -1, 1};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        for (int i = 0; i < 5; i++) {
            map[i] = br.readLine().toCharArray();
        }

        combination(0, 0, 0);
        System.out.println(ans);
    }

    static void combination(int idx, int cnt, int sCnt) {
        if (cnt - sCnt > 3) return;

        if (cnt == 7) {
            if (sCnt >= 4) {
                if (isConnected()) ans++;
            }
            return;
        }

        if (idx == 25) return;

        selected[cnt] = idx;
        combination(idx + 1, cnt + 1, sCnt + (map[idx / 5][idx % 5] == 'S' ? 1 : 0));

        combination(idx + 1, cnt, sCnt);
    }

    static boolean isConnected() {
        boolean[] visited = new boolean[7];
        Deque<Integer> q = new ArrayDeque<>();

        q.add(0);
        visited[0] = true;
        int count = 1;

        while (!q.isEmpty()) {
            int curIdx = q.poll();
            int r = selected[curIdx] / 5;
            int c = selected[curIdx] % 5;

            for (int i = 0; i < 4; i++) {
                int nr = r + dr[i];
                int nc = c + dc[i];

                for (int next = 0; next < 7; next++) {
                    if (!visited[next] && selected[next] / 5 == nr && selected[next] % 5 == nc) {
                        visited[next] = true;
                        count++;
                        q.add(next);
                    }
                }
            }
        }
        return count == 7;
    }
}
```
