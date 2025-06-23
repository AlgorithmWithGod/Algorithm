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

    static int N;
    static long[] F;
    static long T;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        F = new long[N];
        for(int i=0;i<N;i++) F[i] = io.nextInt();
        T = io.nextInt();

    }

    static void solve() throws Exception {

        long div = 0;
        for(int i=0;i<N;i++) div += F[i];

        long[] check = new long[500001];

        for(int i=0;i<N;i++) {
            if(F[i] != 1) check[(int)F[i]]++;
            long prev = F[i];
            for(int j=2;j<=(F[i]-1)/j + 1;j++) {
                long now = (F[i]-1)/j + 1;
                check[j] += prev-now;
                if(now != j) check[(int)now]++;
                prev = now;
            }
        }

        long min = div * (T+1), ans = 1;
        for(int i=2;i<=500000;i++) if(check[i] != 0) {
            div -= check[i];
            long res = div * (T+i);
            if(res < min) {
                min = res;
                ans = i;
            }
        }

        io.write(min + " " + ans);

    }

}
```
