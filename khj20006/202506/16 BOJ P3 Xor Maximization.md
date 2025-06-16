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
    static long[] A;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        A = new long[N];
        for(int i=0;i<N;i++) A[i] = io.nextLong();

    }

    static void solve() throws Exception {

        long[] basis = new long[60];
        for(int i=0;i<N;i++){
            for(int k=59;k>=0;k--) if((A[i] & (1L<<k)) != 0) {
                if(basis[k] == 0) {
                    basis[k] = A[i];
                    break;
                }
                A[i] ^= basis[k];
            }

        }

        long ans = 0;
        for(int k=59;k>=0;k--) ans = Math.max(ans, ans ^ basis[k]);
        io.write(ans + "\n");

    }

}
```
