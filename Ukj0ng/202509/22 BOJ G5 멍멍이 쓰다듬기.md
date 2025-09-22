```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static long X, Y, diff;

    public static void main(String[] args) throws IOException {
        init();
        long answer = solve();
        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        X = Long.parseLong(st.nextToken());
        Y = Long.parseLong(st.nextToken());
        diff = Y - X;
    }

    private static long solve() {
        if (diff == 0) {
            return 0;
        }

        long k = (long) Math.sqrt(diff);

        if (k * k == diff) {
            return 2 * k - 1;
        } else if (diff <= k * k + k) {
            return 2 * k;
        } else {
            return 2 * k + 1;
        }
    }
}
```
