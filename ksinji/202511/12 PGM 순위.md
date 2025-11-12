```java
import java.util.*;

class Solution {
    public int solution(int n, int[][] results) {
        int[][] g = new int[n + 1][n + 1];

        // 이기면 1, 지면 -1, 모르면 0
        for (int[] r : results) {
            int win = r[0], lose = r[1];

            g[win][lose] = 1;
            g[lose][win] = -1;
        }

        for (int k = 1; k <= n; k++) {
            for (int i = 1; i <= n; i++) {
                if (i == k) continue;
                for (int j = 1; j <= n; j++) {
                    if (j == i || j == k) continue;

                    if (g[i][k] == 1 && g[k][j] == 1) {
                        g[i][j] = 1;
                        g[j][i] = -1;
                    }

                    else if (g[i][k] == -1 && g[k][j] == -1) {
                        g[i][j] = -1;
                        g[j][i] = 1;
                    }
                }
            }
        }

        int answer = 0;
        for (int i = 1; i <= n; i++) {
            boolean know = true;
            for (int j = 1; j <= n; j++) {
                if (i == j) continue;
                if (g[i][j] == 0) { 
                    know = false;
                    break;
                }
            }
            if (know) answer++;
        }
        
        return answer;
    }
}
```