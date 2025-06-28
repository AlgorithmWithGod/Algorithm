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

class Segtree {
    int size;
    long[] seg;
    Segtree(int size) {
        this.size = size;
        seg = new long[this.size*4];
    }

    void update(int s, int e, int i, int v, int n) {
        if(s == e) {
            seg[n] = v;
            return;
        }
        int m = (s+e)>>1;
        if(i <= m) update(s,m,i,v,n*2);
        else update(m+1,e,i,v,n*2+1);
        seg[n] = seg[n*2] + seg[n*2+1];
    }

    long find(int s, int e, int l, int r, int n) {
        if(l>r || l>e || r<s) return 0;
        if(l<=s && e<=r) return seg[n];
        int m = (s+e)>>1;
        return find(s,m,l,r,n*2) + find(m+1,e,l,r,n*2+1);
    }

}

public class Main {

    static IOController io;

    //

    static final long MOD = 998244353;

    static int N;
    static int[][] infos;
    static Segtree left, right;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        infos = new int[N][];
        for(int i=1;i<=N;i++){
            int a = io.nextInt();
            infos[i-1] = new int[]{a,i};
        }
        left = new Segtree(N);
        right = new Segtree(N);

    }

    static void solve() throws Exception {

        Arrays.sort(infos, (a,b) -> a[0]==b[0] ? b[1]-a[1] : a[0]-b[0]);

        long ans = 0;
        for(int[] info : infos) {
            int val = info[0], idx = info[1];
            long res1 = left.find(1,N,1,idx-1,1) % MOD * (N-idx+1) % MOD;
            long res2 = right.find(1,N,idx+1,N,1) % MOD * idx % MOD;
            ans = (ans + (res1 + res2) * val) % MOD;
            left.update(1,N,idx,idx,1);
            right.update(1,N,idx,N-idx+1,1);
        }
        io.write(ans + "\n");

    }

}
```
