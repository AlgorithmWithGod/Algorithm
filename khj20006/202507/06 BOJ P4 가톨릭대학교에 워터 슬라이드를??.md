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
    static List<Integer>[] G, R;
    static Stack<Integer> S;
    static int[] C, D;
    static boolean[] vis;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        G = new List[N+1];
        R = new List[N+1];
        for(int i=1;i<=N;i++) {
            G[i] = new ArrayList<>();
            R[i] = new ArrayList<>();
        }

        while(M-- > 0) {
            int a = io.nextInt(), b = io.nextInt();
            G[a].add(b);
            R[b].add(a);
        }

        S = new Stack<>();
        C = new int[N+1];

    }

    static void solve() throws Exception {

        vis = new boolean[N+1];
        for(int i=1;i<=N;i++) if(!vis[i]) {
            vis[i] = true;
            dfs1(i);
        }

        vis = new boolean[N+1];
        int cnt = 0;
        while(!S.isEmpty()) {
            int n = S.pop();
            if(vis[n]) continue;
            vis[n] = true;
            dfs2(n,++cnt);
        }

        D = new int[cnt+1];
        for(int i=1;i<=N;i++) for(int j:G[i]) {
            if(C[i] != C[j]) D[C[j]]++;
        }

        int ans = 0;
        for(int i=1;i<=cnt;i++) if(D[i] == 0) ans++;
        io.write(ans + "\n");

    }

    static void dfs1(int n) {
        for(int i:G[n]) if(!vis[i]) {
            vis[i] = true;
            dfs1(i);
        }
        S.add(n);
    }

    static void dfs2(int n, int c) {
        C[n] = c;
        for(int i:R[n]) if(!vis[i]) {
            vis[i] = true;
            dfs2(i,c);
        }
    }

}
```
