```java
import java.io.*;
import java.util.*;

public class Main {
    static int[][] player = new int[11][11];
    static boolean[] visited = new boolean[11];
    static int res;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int T = Integer.parseInt(br.readLine());

        for (int t = 0; t < T; t++) {
            for (int i = 0; i < 11; i++) {
                st = new StringTokenizer(br.readLine());
                for (int j = 0; j < 11; j++) {
                    player[i][j] = Integer.parseInt(st.nextToken());
                }
            }
            
            res = 0;
            dfs(0, 0);
            System.out.println(res);
        }
    }

    static void dfs(int pos, int temp) {
        if (pos == 11) {
            res = Math.max(res, temp);
            return;
        }

        for (int i = 0; i < 11; i++) {
            if (!visited[i] && player[i][pos] > 0) {
                visited[i] = true;
                dfs(pos + 1, temp + player[i][pos]);
                visited[i] = false;
            }
        }
    }
}
```
