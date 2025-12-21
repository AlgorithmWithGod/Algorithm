```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_30459_현수막_걸기 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M, R;
    private static int[] piles, flagpoles;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());

        piles = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            piles[i] = Integer.parseInt(st.nextToken());
        }

        flagpoles = new int[M];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < M; i++) {
            flagpoles[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(flagpoles);
    }

    private static void sol() throws IOException {
        double maxArea = -1;
        for (int i = 0; i < N; i++) {
            for (int j = i + 1; j < N; j++) {
                int    bottom    = Math.abs(piles[i] - piles[j]);
                double maxHeight = 2.0 * R / bottom;

                int idx = upperBound(maxHeight) - 1;
                if (idx >= 0) {
                    double area = flagpoles[idx] * bottom / 2.0;
                    maxArea = Math.max(maxArea, area);
                }
            }
        }
        bw.write(maxArea > 0 ? String.format("%.1f", maxArea) : "-1");
        bw.flush();
        bw.close();
        br.close();
    }

    private static int upperBound(double target) {
        int left  = 0;
        int right = flagpoles.length;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (flagpoles[mid] > target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }

}
```