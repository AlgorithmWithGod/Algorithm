```java
import java.util.*;
import java.io.*;

class IOController {
    BufferedReader br;
    BufferedWriter bw;
    StringTokenizer st;

    public IOController() {
        br = new BufferedReader(new InputStreamReader(System.in));
        bw = new BufferedWriter(new OutputStreamWriter(System.out));
        st = new StringTokenizer("");
    }

    String nextLine() throws Exception {
        String line = br.readLine();
        st = new StringTokenizer(line);
        return line;
    }

    String nextToken() throws Exception {
        while (!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }

    int nextInt() throws Exception {
        return Integer.parseInt(nextToken());
    }

    long nextLong() throws Exception {
        return Long.parseLong(nextToken());
    }

    double nextDouble() throws Exception {
        return Double.parseDouble(nextToken());
    }

    void close() throws Exception {
        bw.flush();
        bw.close();
    }

    void write(String content) throws Exception {
        bw.write(content);
    }

}

public class Main {

    static IOController io;

    //

    static int N, L;
    static int[][] infos;
    static TreeMap<Integer, Long> h, l;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    static void init() throws Exception {

        N = io.nextInt();
        L = io.nextInt();
        infos = new int[N][2];
        for(int i=0;i<N;i++) for(int j=0;j<2;j++) infos[i][j] = io.nextInt();
        h = new TreeMap<>();
        l = new TreeMap<>();

    }

    static void solve() throws Exception {

        Arrays.sort(infos, (a,b) -> a[1]==b[1] ? a[0]-b[0] : a[1]-b[1]);
        long ans = 0;
        for(int[] info : infos) {
            int t = info[0], d = info[1];
            long hValue = h.getOrDefault(t, 0L);
            long hRes = Math.max(hValue, l.getOrDefault(d,0L) + Math.abs(t-d) + L);
            long lValue = l.getOrDefault(d, 0L);
            long lRes = Math.max(lValue, Math.max(lValue, h.getOrDefault(t, 0L) + Math.abs(t-d) + L));
            h.put(t, hRes);
            l.put(d, lRes);
            ans = Math.max(ans, Math.max(hRes, lRes));
        }
        io.write(ans + "\n");


    }

}
```
