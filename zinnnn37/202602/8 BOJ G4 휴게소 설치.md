```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_1477_휴게소_세우기 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M, L;
    private static int[] rests;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());

        rests = new int[N + 2];
        st = new StringTokenizer(br.readLine());
        for (int i = 1; i <= N; i++) {
            rests[i] = Integer.parseInt(st.nextToken());
        }
        rests[N + 1] = L;
        Arrays.sort(rests);
    }

    private static void sol() throws IOException {
        int left  = 1;
        int right = L - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            int sum = 0;
            for (int i = 1; i <= N + 1; i++) {
                sum += (rests[i] - rests[i - 1] - 1) / mid;
            }

            if (sum > M) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        bw.write(left + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```