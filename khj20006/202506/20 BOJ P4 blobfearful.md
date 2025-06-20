```java
import java.math.BigInteger;
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

    static long K, Q;
    static HashMap<Long, Integer> M;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        K = io.nextLong();
        Q = io.nextInt();
        M = new HashMap<>();

    }

    static void solve() throws Exception {

        for(long k=2;k*k<=K;k++) if(K%k == 0) {
            int cnt = 0;
            while(K%k == 0){
                K/=k;
                cnt++;
            }
            M.put(k, cnt);
        }
        if(K != 1) M.put(K, 1);

        while(Q-->0) {
            long a = io.nextLong();
            long ans = 0;
            for(long i:M.keySet()) {
                long temp = a;
                int cnt = 0;
                while(temp%i == 0){
                    temp /= i;
                    cnt++;
                }
                cnt = Math.max(0, M.get(i) - cnt);
                long res = 0, count = 0;
                while(count < cnt) {
                    res += i;
                    for(long j = i;j<=res;j*=i) if(res % j == 0) count++;
                }
                ans = Math.max(ans, res);
            }
            io.write(ans + " ");
        }

    }

}
```
