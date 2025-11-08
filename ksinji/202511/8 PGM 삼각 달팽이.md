```java
import java.util.*;

class Solution {
    public int[] solution(int n) {
        int total = n * (n + 1) / 2;
        int[][] tri = new int[n][n];

        int num = 1;
        int r = -1;
        int c = 0;
        int len = n;

        while (len > 0) {
            for (int i = 0; i < len; i++) {
                tri[++r][c] = num++;
            }
            len--;
            if (len == 0) break;

            for (int i = 0; i < len; i++) {
                tri[r][++c] = num++;
            }
            len--;
            if (len == 0) break;

            for (int i = 0; i < len; i++) {
                tri[--r][--c] = num++;
            }
            len--;
        }

        int[] answer = new int[total];
        int idx = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j <= i; j++) {
                answer[idx++] = tri[i][j];
            }
        }
        return answer;
    }
}

```
