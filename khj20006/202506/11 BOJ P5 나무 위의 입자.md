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

    void nextLine() throws Exception {
        st = new StringTokenizer(br.readLine());
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
    static List<Integer>[] V;
    static int[] par;
    static int[] OD, OU, ED, EU;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        V = new List[N+1];
        for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
        for(int i=1;i<N;i++) {
            int a = io.nextInt(), b = io.nextInt();
            V[a].add(b);
            V[b].add(a);
        }

        par = new int[N+1];
        OD = new int[N+1];
        OU = new int[N+1];
        ED = new int[N+1];
        EU = new int[N+1];

    }

    static void solve() throws Exception {

        dfs1(1,0);
        dfs2(1,0);

        while(M-->0) {
            int u = io.nextInt(), v = io.nextInt(), c = io.nextInt();
            if(par[v] == u){
                if(c == 0) io.write((OU[v] * OD[v] + EU[v] * ED[v]) + "\n");
                else io.write((OU[v] * ED[v] + EU[v] * OD[v]) + "\n");
            }
            else{
                if(c == 0) io.write((OU[u] * OD[u] + EU[u] * ED[u]) + "\n");
                else io.write((OU[u] * ED[u] + EU[u] * OD[u]) + "\n");
            }
        }

    }

    static void dfs1(int n, int p) {
        par[n] = p;
        for(int i:V[n]) if(i != p) {
            dfs1(i,n);
            OD[n] += ED[i];
            ED[n] += OD[i];
        }
        ED[n]++;
    }

    static void dfs2(int n, int p) {
        if(n != 1) {
            OU[n] = EU[p] + ED[p] - OD[n];
            EU[n] = OU[p] + OD[p] - ED[n];
        }
        for(int i:V[n]) if(i != p) dfs2(i,n);
    }

}
```
