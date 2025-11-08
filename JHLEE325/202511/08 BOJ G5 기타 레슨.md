```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        int[] lectures = new int[N];
        long sum = 0;
        int maxLen = 0;

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            lectures[i] = Integer.parseInt(st.nextToken());
            sum += lectures[i];
            if (lectures[i] > maxLen) {
                maxLen = lectures[i];
            }
        }

        long low = maxLen;
        long high = sum;
        long answer = sum;

        while (low <= high) {
            long mid = (low + high) / 2;

            int cnt = 1;
            long cur = 0;
            for (int i = 0; i < N; i++) {
                if (cur + lectures[i] > mid) {
                    cnt++;
                    cur = lectures[i];
                } else {
                    cur += lectures[i];
                }
            }

            if (cnt > M) {
                low = mid + 1;
            } else {
                answer = mid;
                high = mid - 1;
            }
        }

        System.out.println(answer);
    }
}
```
