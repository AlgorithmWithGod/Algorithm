```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int h = Integer.parseInt(st.nextToken());

        int[] seok = new int[h + 2];
        int[] jong = new int[h + 2];

        for (int i = 0; i < n; i++) {
            int height = Integer.parseInt(br.readLine());
            if (i % 2 == 0) seok[height]++;
            else jong[height]++;
        }

        for (int i = h - 1; i >= 1; i--) {
            seok[i] += seok[i + 1];
            jong[i] += jong[i + 1];
        }

        int min = Integer.MAX_VALUE;
        int count = 0;

        for (int i = 1; i <= h; i++) {
            int crash = seok[i] + jong[h - i + 1];

            if (crash < min) {
                min = crash;
                count = 1;
            } else if (crash == min) {
                count++;
            }
        }

        System.out.println(min + " " + count);
    }
}
```
