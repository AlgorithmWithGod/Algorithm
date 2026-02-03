```java
import java.io.*;
import java.util.*;

public class Main {

    static int n, x, y, count;
    static int[] arr;
    static boolean[] used;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        x = Integer.parseInt(st.nextToken());
        y = Integer.parseInt(st.nextToken());

        arr = new int[2 * n + 1];
        used = new boolean[n + 1];

        int fixedNum = y - x - 1;
        arr[x] = arr[y] = fixedNum;
        used[fixedNum] = true;

        check(1);

        System.out.println(count);
    }

    static void check(int pos) {
        if (pos == 2 * n + 1) {
            count++;
            return;
        }

        if (arr[pos] != 0) {
            check(pos + 1);
            return;
        }

        for (int i = 1; i <= n; i++) {
            if (used[i]) continue;

            if (pos + i + 1 <= 2 * n && arr[pos + i + 1] == 0) {
                arr[pos] = arr[pos + i + 1] = i;
                used[i] = true;

                check(pos + 1);

                arr[pos] = arr[pos + i + 1] = 0;
                used[i] = false;
            }
        }
    }
}
```
