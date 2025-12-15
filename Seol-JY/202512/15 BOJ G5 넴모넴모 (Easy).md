```java
import java.io.*;
import java.util.*;

public class Main {
    static int N, M;
    static boolean[][] grid;
    static long count = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        grid = new boolean[N][M];
        
        backtrack(0);
        System.out.println(count);
    }

    static void backtrack(int pos) {
        if (pos == N * M) {
            count++;
            return;
        }

        int row = pos / M;
        int col = pos % M;

        grid[row][col] = false;
        backtrack(pos + 1);

        grid[row][col] = true;
        if (row > 0 && col > 0 && grid[row-1][col] && grid[row][col-1] && grid[row-1][col-1]) {
            grid[row][col] = false;
            return;
        }
        backtrack(pos + 1);
        grid[row][col] = false;
    }
}
```
