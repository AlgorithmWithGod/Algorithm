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
    static List<int[]>[] graph;
    static int[] down, up;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    static void init() throws Exception {

        N = io.nextInt();
        graph = new ArrayList[N+1];
        for(int i=1;i<=N;i++) graph[i] = new ArrayList<>();
        down = new int[N+1];
        up = new int[N+1];
        for(int i=1;i<N;i++) {
            int a = io.nextInt();
            int b = io.nextInt();
            int c = io.nextInt();
            graph[a].add(new int[]{b,c});
            graph[b].add(new int[]{a,c});
        }

    }

    static void solve() throws Exception {

        dfs1(1,0);
        dfs2(1,0);
        for(int i=1;i<=N;i++) {
            io.write(Math.max(up[i], down[i]) + "\n");
        }

    }

    static void dfs1(int n, int p) {
        for(int[] e:graph[n]) if(e[0] != p) {
            dfs1(e[0],n);
            down[n] = Math.max(down[n], down[e[0]] + e[1]);
        }
    }

    static void dfs2(int n, int p) {
        int max1 = 0, max2 = 0;
        int num1 = 0;
        for(int[] e:graph[n]) if(e[0] != p) {
            if(down[e[0]] + e[1] > max1) {
                max2 = max1;
                max1 = down[e[0]] + e[1];
                num1 = e[0];
            }
            else if(down[e[0]] + e[1] > max2) {
                max2 = down[e[0]] + e[1];
            }
        }
        for(int[] e:graph[n]) if(e[0] != p) {
            if(e[0] == num1) {
                up[e[0]] = Math.max(up[n], max2) + e[1];
            }
            else {
                up[e[0]] = Math.max(up[n], max1) + e[1];
            }
            dfs2(e[0], n);
        }
    }

}
```
