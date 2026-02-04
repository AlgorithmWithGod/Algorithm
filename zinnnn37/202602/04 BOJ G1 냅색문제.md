```java
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.StringTokenizer;

public class BJ_1450_냅색문제 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, C;
    private static int[]      weight;
    private static List<Long> left, right;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());

        weight = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            weight[i] = Integer.parseInt(st.nextToken());
        }

        left = new ArrayList<>();
        right = new ArrayList<>();
    }

    private static void sol() throws IOException {
        int mid = N / 2;

        int leftBit = (1 << mid);
        for (int subset = 0; subset < leftBit; subset++) {
            long sum = 0;
            for (int idx = 0; idx < mid; idx++) {
                if ((subset & (1 << idx)) != 0) {
                    sum += weight[idx];
                }
            }
            if (sum <= C) {
                left.add(sum);
            }
        }

        int rightSize = N - mid;
        int rightBit  = (1 << rightSize);
        for (int subset = 0; subset < rightBit; subset++) {
            long sum = 0;
            for (int idx = 0; idx < rightSize; idx++) {
                if ((subset & (1 << idx)) != 0) {
                    sum += weight[idx + mid];
                }
            }
            if (sum <= C) {
                right.add(sum);
            }
        }

        Collections.sort(right);

        long ans = 0;
        for (long leftSum : left) {
            ans += upperBound(right, C - leftSum);
        }

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static int upperBound(List<Long> list, long target) {
        int start = 0;
        int end   = list.size();

        while (start < end) {
            int mid = (start + end) / 2;
            if (list.get(mid) <= target) {
                start = mid + 1;
            } else {
                end = mid;
            }
        }
        return start;
    }

}
```