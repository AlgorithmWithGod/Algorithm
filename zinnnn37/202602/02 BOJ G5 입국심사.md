```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_3079_입국심사 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M;
    private static int   min;
    private static int[] immigration;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        min = Integer.MAX_VALUE;
        immigration = new int[N];
        for (int i = 0; i < N; i++) {
            immigration[i] = Integer.parseInt(br.readLine());
            min = Math.min(min, immigration[i]);
        }
    }

    private static void sol() throws IOException {
        long left  = 1;
        long right = (long) min * M;
        while (left < right) {
            long mid = left + (right - left) / 2;

            if (canUseImmigration(mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        bw.write(left + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static boolean canUseImmigration(long time) {
        long cnt = 0;
        for (int t : immigration) {
            cnt += time / t;
            if (cnt >= M) return true;
        }
        return cnt >= M;
    }

}
```