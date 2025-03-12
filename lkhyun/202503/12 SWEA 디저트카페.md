```java
import java.util.*;
import java.io.*;

public class Solution {
    static int N, maxCount;
    static int[][] map;
    static boolean[] dessertVisited;
    
    static int[] di = {1, 1, -1, -1};
    static int[] dj = {1, -1, -1, 1};

    public static void main(String[] args) throws Exception {
        //System.setIn(new FileInputStream("sample_input.txt"));
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());
        StringTokenizer st;
        for (int t = 1; t <= T; t++) {
            N = Integer.parseInt(br.readLine());
            map = new int[N][N];
            for (int i = 0; i < N; i++) {
                st = new StringTokenizer(br.readLine());
                for (int j = 0; j < N; j++) {
                    map[i][j] = Integer.parseInt(st.nextToken());
                }
            }
            maxCount = -1;
            
            for (int i = 0; i < N - 1; i++) {
                for (int j = 1; j < N - 1; j++) {
                    dessertVisited = new boolean[101];
                    dessertVisited[map[i][j]] = true;
                    dfs(i, j, i, j, 1, 0, 0);
                }
            }
            System.out.println("#" + t + " " + maxCount);
        }
    }

    static void dfs(int startI, int startJ, int curI, int curJ, int count, int d, int turn) {

        for (int newdirection = d; newdirection <= d + 1 && newdirection < 4; newdirection++) {
            int newi = curI + di[newdirection];
            int newj = curJ + dj[newdirection];

            if (newi < 0 || newi >= N || newj < 0 || newj >= N)
                continue;
            
            if (newi == startI && newj == startJ && count >= 4) {
                maxCount = Math.max(maxCount, count);
                continue;
            }
            if (dessertVisited[map[newi][newj]])
                continue;
            
            dessertVisited[map[newi][newj]] = true;
            dfs(startI, startJ, newi, newj, count + 1, newdirection, (newdirection == d ? turn : turn + 1));
            dessertVisited[map[newi][newj]] = false;
        }
    }
}

```
