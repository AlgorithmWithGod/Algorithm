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

    static int N, M, K;
    static List<int[]>[] V;

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
        V = new List[N+1];
        for(int i=1;i<=N;i++) V[i] = new ArrayList<>();
        for(int i=0;i<M;i++) {
            int a = io.nextInt(), b = io.nextInt(), c = io.nextInt();
            V[a].add(new int[]{b,c});
            V[b].add(new int[]{a,c});
        }

    }

    static void solve() throws Exception {

        int[] D = new int[N+1];
        Arrays.fill(D, (int)1e9);
        PriorityQueue<int[]> Q = new PriorityQueue<>((a,b) -> a[0]-b[0]);
        for(int i=0;i<K;i++) {
            int a = io.nextInt();
            D[a] = 0;
            Q.offer(new int[]{0,a});
        }

        while(!Q.isEmpty()) {
            int[] now = Q.poll();
            int d = now[0], n = now[1];
            if(d > D[n]) continue;
            for(int[] e:V[n]) {
                int i = e[0], c = e[1];
                if(D[i] > d+c) {
                    D[i] = d+c;
                    Q.offer(new int[]{D[i],i});
                }
            }
        }

        int ans = 0;
        for(int n=1;n<=N;n++) for(int[] e:V[n]) {
            int i = e[0], c = e[1];
            if(D[n] + c == D[i]) continue;
            ans = Math.max(Math.max(ans, D[n]*2), Math.max(D[i]*2, (D[n]+D[i]+c)));
        }

        io.write((ans+1)/2 + "\n");

    }

}
```
