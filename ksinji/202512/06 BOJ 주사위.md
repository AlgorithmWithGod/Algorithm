```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        long n = Long.parseLong(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());

        long[] d = new long[6];
        for (int i = 0; i < 6; i++) {
            d[i] = Long.parseLong(st.nextToken());
        }

        if (n == 1) {
            long sum = 0;
            long max = 0;
            for (long v : d) {
                sum += v;
                if (v > max) max = v;
            }
            System.out.println(sum - max);
            return;
        }

        long min1 = Long.MAX_VALUE;
        for (long v : d) {
            if (v < min1) min1 = v;
        }

        long[] p = new long[3];
        p[0] = Math.min(d[0], d[5]);
        p[1] = Math.min(d[1], d[4]);
        p[2] = Math.min(d[2], d[3]);
        Arrays.sort(p);

        long min2 = p[0] + p[1];
        long min3 = p[0] + p[1] + p[2];

        long cnt3 = 4;
        long cnt2 = 8 * (n - 2) + 4;
        long cnt1 = 5 * (n - 2) * (n - 2) + 4 * (n - 2);

        long ans = min1 * cnt1 + min2 * cnt2 + min3 * cnt3;
        System.out.println(ans);
    }
}

```
