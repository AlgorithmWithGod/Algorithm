```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_1253_좋다 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static       StringTokenizer st;

    private static int N, cnt;
    private static long[] arr;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        cnt = 0;

        arr = new long[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Long.parseLong(st.nextToken());
        }
        Arrays.sort(arr);
    }

    private static void sol() {
        for (int i = 0; i < N; i++) {
            if (isGood(i)) {
                cnt++;
            }
        }
        System.out.println(cnt);
    }

    private static boolean isGood(int idx) {
        long target = arr[idx];
        int  left   = 0;
        int  right  = N - 1;

        while (left < right) {
            if (left == idx) {
                left++;
                continue;
            } else if (right == idx) {
                right--;
                continue;
            }

            long current = arr[left] + arr[right];

            if (current == target) {
                return true;
            } else if (current < target) {
                left++;
            } else {
                right--;
            }
        }

        return false;
    }

}
```
