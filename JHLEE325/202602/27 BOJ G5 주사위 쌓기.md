```java
import java.io.*;
import java.util.*;

public class Main {
    static int N;
    static int[][] dice;
    static int[] pair = {5, 3, 4, 1, 2, 0};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        dice = new int[N][6];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 6; j++) {
                dice[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        int maxTotal = 0;

        for (int i = 1; i <= 6; i++) {
            maxTotal = Math.max(maxTotal, solve(i));
        }

        System.out.println(maxTotal);
    }

    static int solve(int firstnum) {
        int sideSum = 0;
        int curBottom = firstnum;

        for (int i = 0; i < N; i++) {
            int bottomIdx = 0;
            for (int j = 0; j < 6; j++) {
                if (dice[i][j] == curBottom) {
                    bottomIdx = j;
                    break;
                }
            }

            int topIdx = pair[bottomIdx];
            int topNum = dice[i][topIdx];

            int sideMax = 0;
            for (int j = 0; j < 6; j++) {
                if (j == bottomIdx || j == topIdx) continue;
                sideMax = Math.max(sideMax, dice[i][j]);
            }

            sideSum += sideMax;
            curBottom = topNum;
        }

        return sideSum;
    }
}
```
