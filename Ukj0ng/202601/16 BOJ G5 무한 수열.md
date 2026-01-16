```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Map<Long, Long> map;
    private static int P, Q;
    private static long N;

    public static void main(String[] args) throws IOException {
        init();

        long answer = backTracking(N);
        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Long.parseLong(st.nextToken());
        P = Integer.parseInt(st.nextToken());
        Q = Integer.parseInt(st.nextToken());

        map = new HashMap<>();
    }

    private static long backTracking(long n) {
        if (n == 0) return 1;
        if (map.containsKey(n)) return map.get(n);

        long temp = backTracking(n/P) + backTracking(n/Q);
        map.put(n, temp);
        return temp;
    }
}
```
