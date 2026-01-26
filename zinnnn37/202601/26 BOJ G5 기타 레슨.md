```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_2343_기타_레슨 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, M, left, right, ans;
    private static int[] lessons;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        left = right = 0;
        ans = Integer.MAX_VALUE;
        lessons = new int[N];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            lessons[i] = Integer.parseInt(st.nextToken());
            left = Math.max(left, lessons[i]);
            right += lessons[i];
        }
    }

    private static void sol() throws IOException {
        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (isRecordable(mid)) {
                ans = Math.min(ans, mid);
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static boolean isRecordable(int mid) {
        int cnt = 1;
        int sum = 0;

        for (int lesson : lessons) {
            if (sum + lesson <= mid) {
                sum += lesson;
            } else {
                cnt++;
                sum = lesson;
            }
        }

        return cnt <= M;
    }

}
```
