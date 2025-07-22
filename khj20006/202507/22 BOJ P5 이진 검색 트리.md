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

    static final int INF = (int)1e9 + 7;

    static int N;
    static int[] dep, idx;
    static TreeSet<Integer> set;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        dep = new int[N];
        idx = new int[N];
        set = new TreeSet<>();

    }

    static void solve() throws Exception {

        set.add(io.nextInt());
        long ans = 1;
        for(int i=1;i<N;i++) {
            int a = io.nextInt();
            int right = set.higher(a) == null ? -1 : set.higher(a);
            int left = set.lower(a) == null ? -1 : set.lower(a);
            if(right == -1) dep[a] = dep[left]+1;
            else if(left == -1) dep[a] = dep[right]+1;
            else {
                if(idx[left] > idx[right]) dep[a] = dep[left]+1;
                else dep[a] = dep[right]+1;
            }
            ans += dep[a]+1;
            idx[a] = i;
            set.add(a);
        }
        io.write(ans + "\n");

    }

}
```
