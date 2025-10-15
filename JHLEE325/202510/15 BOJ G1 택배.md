```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int c = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(br.readLine());
        int[][] express = new int[m][3];

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int from = Integer.parseInt(st.nextToken());
            int to = Integer.parseInt(st.nextToken());
            int box = Integer.parseInt(st.nextToken());
            express[i][0] = from;
            express[i][1] = to;
            express[i][2] = box;
        }

        Arrays.sort(express, (a, b) -> {
            if (a[1] == b[1]) return a[0] - b[0];
            return a[1] - b[1];
        });

        int[] load = new int[n + 1];
        int result = 0;

        for (int i = 0; i < m; i++) {
            int from = express[i][0];
            int to = express[i][1];
            int box = express[i][2];

            int maxbox = 0;
            for (int j = from; j < to; j++) {
                maxbox = Math.max(maxbox, load[j]);
            }

            int canbox = Math.min(c - maxbox, box);
            if (canbox <= 0) continue;

            for (int j = from; j < to; j++) {
                load[j] += canbox;
            }

            result += canbox;
        }

        System.out.println(result);
    }
}
```
