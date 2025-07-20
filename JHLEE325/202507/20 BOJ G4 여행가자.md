```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        int m = Integer.parseInt(br.readLine());

        int[][] map = new int[n][n];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < n; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                if (i == j) {
                    map[i][j] = 1;
                }
            }
        }

        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (map[i][k] == 1 && map[k][j] == 1)
                        map[i][j] = 1;
                }
            }
        }

        int[] route = new int[m];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < m; i++) {
            route[i] = Integer.parseInt(st.nextToken());
        }

        if (m == 1) {
            System.out.println("YES");
            return;
        }

        for (int i = 0; i < m - 1; i++) {
            if (map[route[i] - 1][route[i + 1] - 1] == 0) {
                System.out.println("NO");
                return;
            }
        }
        System.out.println("YES");
    }
}
```
