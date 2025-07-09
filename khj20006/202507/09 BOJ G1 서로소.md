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

    static long A, B, N;
    static List<Long> list;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        int TC = io.nextInt();
        for(int tc=1;tc<=TC;tc++) {
            io.write("Case #" + tc + ": ");
            init();
            solve();
        }

        io.close();

    }

    public static void init() throws Exception {

        A = io.nextLong();
        B = io.nextLong();
        N = io.nextLong();

    }

    static void solve() throws Exception {

        list = new ArrayList<>();
        for(long i=2;i*i<=N;i++) if(N%i == 0) {
            while(N%i == 0) N/=i;
            list.add(i);
        }
        if(N != 1) list.add(N);

        io.write((f(B) - f(A-1)) + "\n");

    }

    static long f(long x) {

        long res = x;
        int size = list.size();
        for(int i=1;i<(1<<size);i++) {
            int cnt = 0;
            long v = 1;
            for(int j=0;j<size;j++) if((i & (1<<j)) != 0) {
                v *= list.get(j);
                cnt++;
            }
            if(cnt%2 == 1) res -= x/v;
            else res += x/v;
        }
        return res;

    }

}
```
