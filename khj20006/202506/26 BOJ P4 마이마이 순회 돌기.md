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

    static int N, Q;
    static int[] C, A;
    static long[] sum, cnt;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        Q = io.nextInt();
        C = new int[100001];
        A = new int[N+Q+1];
        for(int i=1;i<=N;i++) {
            A[i] = io.nextInt();
            C[A[i]]++;
        }
        sum = new long[262144];
        cnt = new long[262144];

    }

    static void solve() throws Exception {

        init(1,100000,1);
        while(Q-->0) {
            int op = io.nextInt();
            if(op == 1) {
                int j = io.nextInt(), v = io.nextInt();
                query(1,100000,A[j],-1,1);
                A[j] = v;
                query(1, 100000, A[j], 1, 1);
            }
            else if(op == 2) {
                int T = io.nextInt();
                int idx = find(1,100000,T,1);
                long ans = findcnt(1,100000,1,idx-1,1);
                long res = findsum(1,100000,1,idx-1,1);
                T -= res;
                // idx를 몇 개 가져올 수 있는지?
                ans += Math.min(T/idx, findcnt(1,100000,idx,idx,1));
                io.write(ans + "\n");
            }
            else {
                A[++N] = io.nextInt();
                query(1,100000,A[N],1,1);
            }
        }

    }

    static void init(int s, int e, int n) {
        if(s == e) {
            sum[n] = (long)C[s]*s;
            cnt[n] = C[s];
            return;
        }
        int m=(s+e)>>1;
        init(s,m,n*2);
        init(m+1,e,n*2+1);
        sum[n] = sum[n*2] + sum[n*2+1];
        cnt[n] = cnt[n*2] + cnt[n*2+1];
    }

    static void query(int s, int e, int i, int v, int n) {
        if(s == e) {
            sum[n] += v*s;
            if(v > 0) cnt[n]++;
            else cnt[n]--;
            return;
        }
        int m = (s+e)>>1;
        if(i <= m) query(s,m,i,v,n*2);
        else query(m+1,e,i,v,n*2+1);
        sum[n] = sum[n*2] + sum[n*2+1];
        cnt[n] = cnt[n*2] + cnt[n*2+1];
    }

    static int find(int s, int e, long v, int n) {
        if(s == e) return s;
        int m = (s+e)>>1;
        if(v <= sum[n*2]) return find(s,m,v,n*2);
        return find(m+1,e,v-sum[n*2],n*2+1);
    }

    static long findsum(int s, int e, int l, int r, int n) {
        if(l>r || l>e || r<s) return 0;
        if(l<=s && e<=r) return sum[n];
        int m=(s+e)>>1;
        return findsum(s,m,l,r,n*2) + findsum(m+1,e,l,r,n*2+1);
    }

    static long findcnt(int s, int e, int l, int r, int n) {
        if(l>r || l>e || r<s) return 0;
        if(l<=s && e<=r) return cnt[n];
        int m=(s+e)>>1;
        return findcnt(s,m,l,r,n*2) + findcnt(m+1,e,l,r,n*2+1);
    }

}
```
