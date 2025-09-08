```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        int[] immigration = new int[n];

        for (int i = 0; i < n; i++) {
            immigration[i] = Integer.parseInt(br.readLine());
        }

        long left = 1;
        long right = 1000000000 * (long)m;
        long res = 0;

        while (left <= right) {
            long mid = (left + right) / 2;
            long people = 0;
            for (int i = 0; i < n; i++) {
                people += mid / immigration[i];
                if (people >= m) break;
            }
            if (people >= m) {
                res = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        System.out.println(res);
    }
}
```
