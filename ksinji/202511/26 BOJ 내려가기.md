```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        int n = Integer.parseInt(br.readLine());
        int[][] map = new int[n][3];
        int[] maxdp = new int[3];
        int[] mindp = new int[3];

        for (int i=0; i<n; i++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j=0; j<3; j++){
                int num = Integer.parseInt(st.nextToken());
                if (i==0) {
                    maxdp[j] = num;
                    mindp[j] = num;
                }
                map[i][j] = num;
            }
        }

        for (int i=1; i<n; i++){
            int max1 = Math.max(maxdp[0], maxdp[1]);
            int max2 = Math.max(maxdp[1], maxdp[2]);
            maxdp[0] = max1 + map[i][0];
            maxdp[2] = max2 + map[i][2];

            int max3 = Math.max(max1, max2);
            maxdp[1] = max3 + map[i][1];

            int min1 = Math.min(mindp[0], mindp[1]);
            int min2 = Math.min(mindp[1], mindp[2]);
            mindp[0] = min1 + map[i][0];
            mindp[2] = min2 + map[i][2];

            int min3 = Math.min(min1, min2);
            mindp[1] = min3 + map[i][1];
        }

        int min = Integer.MAX_VALUE;
        int max = 0;
        for (int i=0; i<3; i++){
            min = Math.min(min, mindp[i]);
            max = Math.max(max, maxdp[i]);
        }

        System.out.print(max+" "+min);
    }
}
```
