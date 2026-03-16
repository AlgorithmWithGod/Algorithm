```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int M = Integer.parseInt(st.nextToken());
        int N = Integer.parseInt(st.nextToken());
        int L = Integer.parseInt(st.nextToken());

        int[] guns = new int[M];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
            guns[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(guns);

        int count = 0;
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            if (y > L) continue;

            int low = 0;
            int high = M - 1;

            while (low <= high) {
                int mid = (low + high) / 2;

                long dist = (long) Math.abs(guns[mid] - x) + y;

                if (dist <= L) {
                    count++;
                    break;
                }

                if (guns[mid] < x) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }

        System.out.println(count);
    }
}
```
