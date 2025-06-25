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
    static int[] A, seg;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        A = new int[N+1];
        for(int i=1;i<=N;i++) A[i] = io.nextInt();
        seg = new int[4*N];

    }

    static void solve() throws Exception {

        init(1,N,1);
        int[] ans = new int[N+1];
        for(int i=N;i>=1;i--) {
            int a = A[i];
            int idx = find(1,N,a+1,1);
            ans[idx] = i;
        }
        
        for(int i=1;i<=N;i++) io.write(ans[i] + " ");

    }
    
    static void init(int s, int e, int n) {
        if(s == e) {
            seg[n] = 1;
            return;
        }
        int m=(s+e)>>1;
        init(s,m,n*2);
        init(m+1,e,n*2+1);
        seg[n] = seg[n*2] + seg[n*2+1];
    }
    
    static int find(int s, int e, int v, int n) {
        if(s == e) {
            seg[n]--;
            return s;
        }
        int ret = -1;
        int m = (s+e)>>1;
        if(v > seg[n*2+1]) ret = find(s,m,v-seg[n*2+1],n*2);
        else ret = find(m+1,e,v,n*2+1);
        seg[n] = seg[n*2] + seg[n*2+1];
        return ret;
    }

}
```
