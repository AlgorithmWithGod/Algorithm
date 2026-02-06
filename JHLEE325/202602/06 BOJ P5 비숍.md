```java
import java.io.*;
import java.util.*;

public class Main {
    
    static int n;
    static int[][] board;
    static boolean[] diag1;
    static boolean[] diag2;
    static int[] maxCount = new int[2]; // 0: 검은색, 1: 흰색

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        board = new int[n][n];

        diag1 = new boolean[2 * n];
        diag2 = new boolean[2 * n];

        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < n; j++) {
                board[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        backtracking(0, 0, 0, 0);
        backtracking(0, 1, 0, 1);

        System.out.println(maxCount[0] + maxCount[1]);
    }
    
    static void backtracking(int r, int c, int count, int color) {
        maxCount[color] = Math.max(maxCount[color], count);

        if (c >= n) {
            r++;
            c = (c % 2 == 0) ? 1 : 0;
        }

        if (r >= n) return;

        if (board[r][c] == 1 && !diag1[r + c] && !diag2[r - c + n]) {
            diag1[r + c] = true;
            diag2[r - c + n] = true;
            backtracking(r, c + 2, count + 1, color);
            diag1[r + c] = false;
            diag2[r - c + n] = false;
        }

        backtracking(r, c + 2, count, color);
    }
}
```
