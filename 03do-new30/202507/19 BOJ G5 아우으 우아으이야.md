```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        StringTokenizer st;

        int sum = 0;
        boolean first = true;
        int left = 0;
        int right = 0;

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            if (first) {
                left = x;
                right = y;
                sum += y - x;
                first = false;
                continue;
            }

            if (right <= x) {
                sum += y - x;
                left = x;
                right = y;
            } else {
                if (y < right) continue;
                int tmp = y - right;
                sum += tmp;
                right = y;
            }
        }
        System.out.println(sum);
        br.close();
    }
}
```
