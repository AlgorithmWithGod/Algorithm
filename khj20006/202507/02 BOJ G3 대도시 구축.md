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
    static int[][] infos;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        M = io.nextInt();
        infos = new int[M][];
        for(int i=0;i<M;i++) infos[i] = new int[]{io.nextInt(), io.nextInt()};

    }

    static void solve() throws Exception {

        Arrays.sort(infos, (a,b) -> a[0]==b[0] ? a[1]-b[1] : a[0]-b[0]);
        long ans = (long)N*(N+1)/2 + N-2;

        if(M == 1) {
            if(infos[0][0] == 1) {
                if(infos[0][1] == 2) ans += 2;
                else ans++;
            }
        }
        else if(M == 2) {
            int a = infos[0][0], b = infos[0][1];
            int aa = infos[1][0], bb = infos[1][1];
            if(a == 1 && aa == 1) {
                if(b == 2) {
                    if(bb == 3) ans += 4;
                    else ans += 3;
                }
                else ans += 2;
            }
            else if(a == 1) {
                if(b == 2) {
                    if(aa == 2 && bb == 3) ans += 3;
                    else ans += 2;
                }
                else {
                    if(aa == 2 && b == bb) {
                        if(b == 3) ans += 3;
                        else ans += 2;
                    }
                    else ans++;
                }
            }
        }

        io.write(ans + "\n");

    }

}
```
