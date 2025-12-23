```java
import java.io.*;

public class BJ_2118_두_개의_탑 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    private static int N, ans, half;
    private static int[] dist;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        ans = 0;
        dist = new int[2 * N];

        for (int i = 0; i < N; i++) {
            dist[i] = Integer.parseInt(br.readLine());
            dist[i + N] = dist[i];
            half += dist[i];
        }
        half /= 2;
    }

    private static void sol() throws IOException {
        int left    = 0;
        int right   = 0;
        int curDist = 0;

        while (left < N) {
            while (true) {
                curDist += dist[right++];
                if (curDist > half) {
                    curDist -= dist[--right];
                    break;
                }
            }

            ans = Math.max(ans, curDist);
            curDist -= dist[left++];
        }
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```