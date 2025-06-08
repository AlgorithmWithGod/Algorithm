```java
import java.util.*;
import java.io.*;

public class Main {

    // IO field
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st = new StringTokenizer("");

    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static String nextToken() throws Exception {
        while(!st.hasMoreTokens()) nextLine();
        return st.nextToken();
    }
    static int nextInt() throws Exception { return Integer.parseInt(nextToken()); }
    static long nextLong() throws Exception { return Long.parseLong(nextToken()); }
    static double nextDouble() throws Exception { return Double.parseDouble(nextToken()); }
    static void bwEnd() throws Exception {bw.flush();bw.close();}

    // Additional field

    static int N;
    static long[] A;
    static PriorityQueue<long[]> Q;

    public static void main(String[] args) throws Exception {

        ready();
        solve();

        bwEnd();

    }

    static void ready() throws Exception {

        N = nextInt();
        A = new long[N+1];
        for(int i=1;i<=N;i++) A[i] = nextInt();
        Q = new PriorityQueue<>((a,b) -> Long.compare(a[0]*a[1], b[0]*b[1]));

    }

    static void solve() throws Exception {

        if(N == 1){
            bw.write("0");
            return;
        }

        long ans = 0;
        for(int i=1;i<=N;i++){
            ans += A[i];
            Q.offer(new long[]{A[i], 3});
        }
        for(int i=2;i<N;i++){
            long[] x = Q.poll();
            ans += x[0]*x[1];
            Q.offer(new long[]{x[0], x[1]+2});
        }
        bw.write(ans + "\n");

    }

}
```
