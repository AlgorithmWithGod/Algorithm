```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());

        int[][] map = new int[n][3];
        int[][] dpmax = new int[n][3];
        int[][] dpmin = new int[n][3];

        for (int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 3; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
                if (i == 0) {
                    dpmax[i][j] = dpmin[i][j] = map[i][j];
                }
            }
        }

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < 3; j++) {
                if (j == 0) {
                    dpmax[i][j] = Math.max(dpmax[i - 1][j], dpmax[i - 1][j + 1]) + map[i][j];
                    dpmin[i][j] = Math.min(dpmin[i - 1][j], dpmin[i - 1][j + 1]) + map[i][j];
                } else if (j == 1) {
                    dpmax[i][j] = Math.max(Math.max(dpmax[i - 1][j], dpmax[i - 1][j + 1]), dpmax[i - 1][j - 1]) + map[i][j];
                    dpmin[i][j] = Math.min(Math.min(dpmin[i - 1][j], dpmin[i - 1][j + 1]), dpmin[i - 1][j - 1]) + map[i][j];
                } else {
                    dpmax[i][j] = Math.max(dpmax[i - 1][j], dpmax[i - 1][j - 1]) + map[i][j];
                    dpmin[i][j] = Math.min(dpmin[i - 1][j], dpmin[i - 1][j - 1]) + map[i][j];
                }
            }
        }

        System.out.println(Math.max(Math.max(dpmax[n - 1][0], dpmax[n - 1][1]), dpmax[n - 1][2]) + " " + Math.min(Math.min(dpmin[n - 1][0], dpmin[n - 1][1]), dpmin[n - 1][2]));
    }
}
```
