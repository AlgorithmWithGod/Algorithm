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
    static int[] r;
    static int[][] info;
    static long[] c;
    
    static int f(int x) {return x==r[x] ? x : (r[x]=f(r[x]));}

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        r = new int[N];
        c = new long[N];
        info = new int[N][];
        for(int i=0;i<N;i++) {
            r[i] = i;
            int a = io.nextInt();
            info[i] = new int[]{a,i};
            c[i] = 1;
        }

    }

    static void solve() throws Exception {

        boolean[] vis = new boolean[N];
        Arrays.sort(info, (a,b) -> b[0]-a[0]);
        
        long ans = 0;
        
        for(int[] f:info) {
            int h = f[0], i = f[1];
            if(i<N-1 && vis[i+1]) {
                int right = f(i+1), cur = f(i);
                c[cur] += c[right];
                r[right] = cur;
            }
            if(i-1>=0 && vis[i-1]) {
                int left = f(i-1), cur = f(i);
                c[cur] += c[left];
                r[left] = cur;
            }
            vis[i] = true;
            ans = Math.max(ans, c[f(i)] * h);
        }
        io.write(ans + "\n");

    }

}
```
