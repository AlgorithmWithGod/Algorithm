```java
import java.io.*;
import java.util.*;

public class Main {
    static int n, k;
    static int[] str;
    static boolean[] robot;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        k = Integer.parseInt(st.nextToken());

        str = new int[2 * n];
        robot = new boolean[n];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < 2 * n; i++) {
            str[i] = Integer.parseInt(st.nextToken());
        }

        int stage = 0;
        while (true) {
            stage++;

            int laststr = str[2 * n - 1];
            for (int i = 2 * n - 1; i > 0; i--) {
                str[i] = str[i - 1];
            }
            str[0] = laststr;

            for (int i = n - 1; i > 0; i--) {
                robot[i] = robot[i - 1];
            }
            robot[0] = false;

            if (robot[n - 1]) {
                robot[n - 1] = false;
            }

            for (int i = n - 2; i >= 0; i--) {
                if (robot[i] && !robot[i + 1] && str[i + 1] >= 1) {
                    robot[i] = false;
                    robot[i + 1] = true;
                    str[i + 1]--;
                }
            }

            if (robot[n - 1]) {
                robot[n - 1] = false;
            }

            if (str[0] > 0) {
                robot[0] = true;
                str[0]--;
            }

            int zerostr = 0;
            for (int d : str) {
                if (d == 0) {
                    zerostr++;
                }
            }
            if (zerostr >= k) {
                break;
            }
        }

        System.out.println(stage);
    }
}
```
