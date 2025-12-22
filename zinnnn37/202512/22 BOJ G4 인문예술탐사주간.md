```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_23829_인물예술탐사주간 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder   sb = new StringBuilder();
    private static       StringTokenizer st;

    private static int N, Q;
    private static int[]  trees;
    private static long[] prefix;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        Q = Integer.parseInt(st.nextToken());

        trees = new int[N + 1];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            trees[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(trees, 1, N + 1);

        prefix = new long[N + 1];
        for (int i = 1; i <= N; i++) {
            prefix[i] = prefix[i - 1] + trees[i];
        }
    }

    private static void sol() throws IOException {
        while (Q-- > 0) {
            int photo = Integer.parseInt(br.readLine());

            int idx      = upperBound(photo);
            int lowerCnt = idx - 1;
            int upperCnt = N - lowerCnt;

            long lowerSum = (long) photo * lowerCnt - prefix[lowerCnt];
            long upperSum = (prefix[N] - prefix[lowerCnt]) - (long) photo * upperCnt;

            sb.append(lowerSum + upperSum).append("\n");
        }
        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

    private static int upperBound(int target) {
        int left  = 1;
        int right = N + 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (trees[mid] <= target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }

}
```