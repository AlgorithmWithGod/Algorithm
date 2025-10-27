```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        long N = Long.parseLong(br.readLine());
        long[] d = new long[6];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < 6; i++) {
            d[i] = Long.parseLong(st.nextToken());
        }

        if (N == 1) {
            long sum = 0, maxv = 0;
            for (int i = 0; i < 6; i++) {
                sum += d[i];
                if (d[i] > maxv) maxv = d[i];
            }
            System.out.println(sum - maxv);
            return;
        }

        long min1 = Long.MAX_VALUE;
        for (int i = 0; i < 6; i++) min1 = Math.min(min1, d[i]);

        long min2 = Long.MAX_VALUE;
        for (int i = 0; i < 6; i++) {
            for (int j = i + 1; j < 6; j++) {
                if (i + j == 5) continue;
                min2 = Math.min(min2, d[i] + d[j]);
            }
        }
        int[][] corners = {
                {0, 1, 2}, {0, 1, 3}, {0, 4, 2}, {0, 4, 3},
                {5, 1, 2}, {5, 1, 3}, {5, 4, 2}, {5, 4, 3}
        };
        long min3 = Long.MAX_VALUE;
        for (int[] c : corners) {
            long sum = d[c[0]] + d[c[1]] + d[c[2]];
            if (sum < min3) min3 = sum;
        }

        long res = 0;
        res += 4 * min3;
        res += (8 * N - 12) * min2;
        res += (5 * N * N - 16 * N + 12) * min1;

        System.out.println(res);
    }
}
```
