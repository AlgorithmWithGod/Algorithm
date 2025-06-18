```java
import java.math.BigInteger;
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

    static int N, M, K, base;
    static List<Integer> A;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        K = io.nextInt();

        boolean[] ex = new boolean[4*N+1];
        for(int i=0;i<M;i++) {
            ex[io.nextInt()] = true;
            ex[io.nextInt()] = true;
        }

        int a = io.nextInt(), b = io.nextInt();
        ex[a] = true;
        ex[b] = true;
        base = Math.abs((a%K) - (b%K));

        A = new ArrayList<>();
        for(int i=1;i<=4*N;i++) if(!ex[i]) A.add(i%K);

    }

    static void solve() throws Exception {

        Collections.sort(A);
        int e = A.size() - 1, s = A.size()/2, ans = 0;
        while(s >= 0) {
            int a = A.get(e), b = A.get(s);
            if(a-b > base) {
                e--;
                ans++;
            }
            s--;
        }
        io.write(Math.min(ans, M-1) + "\n");


    }

}
```
