```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int MAX = 1000000;
    private static long[] f, g;
    private static int N;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());
        f = new long[MAX+1];
        g = new long[MAX+1];

        Arrays.fill(f, 1);

        for (int i = 2; i <= MAX; i++) {
            for (int j = 1; i*j <= MAX; j++) {
                f[i*j] += i;
            }
        }

        for (int i = 1; i <= MAX; i++) {
            g[i] = g[i-1]+f[i];
        }

        while (T-->0) {
            init();
            bw.write(g[N] + "\n");
        }

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
    }
}
```
