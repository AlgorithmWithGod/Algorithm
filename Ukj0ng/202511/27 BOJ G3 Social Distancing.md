```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final long INF = (long)1e18;
    private static long[][] grass;
    private static int N, M;
    public static void main(String[] args) throws IOException {
        init();
        long answer = binarySearch();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        grass = new long[M][2];

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            grass[i][0] = Long.parseLong(st.nextToken());
            grass[i][1] = Long.parseLong(st.nextToken());
        }

        Arrays.sort(grass, (o1, o2) -> Long.compare(o1[0], o2[0]));
    }

    public static long binarySearch() {
        long left = 0;
        long right = INF;
        long result = -1;

        while (left <= right) {
            long mid = left + (right - left) / 2;

            if (valid(mid)) {
                result = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return result;
    }

    private static boolean valid(long target) {
        long count = 0;
        long pos = -INF;

        for (long[] e : grass) {
            long nextPos = pos + target;

            if (nextPos > e[1]) continue;

            nextPos = Math.max(nextPos, e[0]);

            long canPlace = (e[1] - nextPos) / target + 1;
            count += canPlace;

            pos = nextPos + (canPlace - 1) * target;
        }

        return count >= N;
    }
}
```
