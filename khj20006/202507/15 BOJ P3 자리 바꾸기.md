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

class Node {
    int x, y, z;
    Node(int x, int y, int z) {
        this.x = x;
        this.y = y;
        this.z = z;
    }

}

public class Main {

    static IOController io;

    //

    static int N, K;
    static int[] a;
    static int[] cnt;
    static int[][] dist;

    static long ans = 0;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        K = io.nextInt();
        a = new int[N];
        cnt = new int[K+1];
        dist = new int[K+1][N];
        for(int i=0;i<N;i++) {
            a[i] = io.nextInt();
            dist[a[i]][0] += i - cnt[a[i]];
            cnt[a[i]]++;
        }

    }

    static void solve() throws Exception {

        for(int k=1;k<=K;k++) {
            int x = dist[k][0];
            int c = cnt[k];
            for(int i=1;i<N;i++) {
                x -= c;
                if(a[i] == k) c--;
                dist[k][i] = x;
            }
        }

        ans = Long.MAX_VALUE;
        perm(0, 0, new ArrayList<>());
        io.write(ans + "\n");

    }

    static void perm(int count, int state, List<Integer> list) {
        if(count == K) {
            int idx = 0;
            long res = 0;
            for(int i:list) {
                res += dist[i][idx];
                idx += cnt[i];
            }
            ans = Math.min(ans, res);
            return;
        }
        for(int i=1;i<=K;i++) if((state & (1<<i)) == 0) {
            list.add(i);
            perm(count+1, state | (1<<i), list);
            list.remove(list.size()-1);
        }
    }

}
```
