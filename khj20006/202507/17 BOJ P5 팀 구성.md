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

    static int N, K;
    static int[][] infos;

    public static void main(String[] args) throws Exception {

        io = new IOController();

        init();
        solve();

        io.close();

    }

    public static void init() throws Exception {

        N = io.nextInt();
        K = io.nextInt();
        infos = new int[N][];
        for(int i=0;i<N;i++) infos[i] = new int[]{io.nextInt(),io.nextInt()};

    }

    static void solve() throws Exception {

        Arrays.sort(infos, (a,b) -> a[1]==b[1] ? a[0]-b[0] : a[1]-b[1]);
        int[] a = new int[N+1];
        int[] b = new int[N+1];
        for(int i=0;i<N;i++) {
            a[i+1] = infos[i][0];
            b[i+1] = infos[i][1];
        }
        long[] dp = new long[N+1];
        long[] max = new long[N+1];
        for(int i=3;i<=N;i++) {
            dp[i] = max[i-1];
            if(b[i] - b[i-2] <= K) {
                dp[i] = Math.max(dp[i], max[i-3] + a[i-2] + a[i-1] + a[i]);
            }

            if(i >= 4 && b[i] - b[i-3] <= K) {
                List<Integer> list1 = new ArrayList<>();
                for(int j=i-3;j<=i;j++) list1.add(a[j]);
                Collections.sort(list1);
                dp[i] = Math.max(dp[i], max[i-4] + a[i-3] + a[i-2] + a[i-1] + a[i] - list1.get(0));

                if(i >= 5 && b[i] - b[i-4] <= K) {
                    list1 = new ArrayList<>();
                    for(int j=i-4;j<=i;j++) list1.add(a[j]);
                    Collections.sort(list1);
                    dp[i] = Math.max(dp[i], max[i-5] + a[i-4] + a[i-3] + a[i-2] + a[i-1] + a[i] - list1.get(0) - list1.get(1));
                }
            }

            max[i] = Math.max(max[i-1], dp[i]);
        }
        io.write(max[N] + "\n");

    }

}
```
