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

    static int N, M;
    static int[] r;
    static long[] c;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        while(true) {
            N = io.nextInt();
            M = io.nextInt();
            if(N == 0) break;
            init();
            solve();
        }

        io.close();

    }

    static int f(int x) {
        if(x == r[x]) return x;
        int p = f(r[x]);
        c[x] += c[r[x]];
        return (r[x] = p);
    }

    public static void init() throws Exception {

        r = new int[N+1];
        for(int i=1;i<=N;i++) r[i] = i;
        c = new long[N+1];

    }

    static void solve() throws Exception {

        while(M-->0) {

            char op = io.nextToken().charAt(0);
            int a = io.nextInt(), b = io.nextInt();

            if(op == '!') {
                int w = io.nextInt();
                int x = f(a), y = f(b);
                if(x == y) continue;
                c[y] = c[a]-c[b]+w;
                r[y] = x;
            }
            else {
                int x = f(a), y = f(b);
                if(x != y) io.write("UNKNOWN\n");
                else io.write((c[b] - c[a]) + "\n");
            }

        }

    }

}
```
