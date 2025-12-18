```java
import java.sql.Array;
import java.util.*;
import java.io.*;

public class Main {

    static BufferedReader br;
    static BufferedWriter bw;
    static StringTokenizer st;

    static int N, M;
    static long[] toggle;
    static List<long[]> results;
    static List<long[]> leftResults;
    static Map<Long, Integer> rightResults;

    public static void main(String[] args) throws Exception {

        input();
        solve();

    }

    public static void input() throws Exception {
        br = new BufferedReader(new InputStreamReader(System.in));

        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        toggle = new long[N];
        for(int i=0;i<N;i++) toggle[i] = (1L<<i);
        for(int i=0;i<M;i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken()) - 1;
            int b = Integer.parseInt(st.nextToken()) - 1;
            toggle[a] |= (1L<<b);
            toggle[b] |= (1L<<a);
        }

        br.close();
    }

    public static void solve() throws Exception {
        bw = new BufferedWriter(new OutputStreamWriter(System.out));

        results = new ArrayList<>();
        bck(0, N/2, 0, 0);
        leftResults = new ArrayList<>();
        leftResults.addAll(results);

        results = new ArrayList<>();
        bck(N/2, N, 0, 0);
        rightResults = new TreeMap<>();
        for(long[] info : results) {
            long status = info[0];
            int cnt = (int)info[1];
            if(!rightResults.containsKey(status) || rightResults.get(status) > cnt) rightResults.put(status, cnt);
        }

        long ans = N;
        for(long[] info : leftResults) {
            long leftStatus = info[0];
            int cntLeft = (int)info[1];
            long target = ((1L<<N)-1) ^ leftStatus;
            int cntRight = rightResults.getOrDefault(target, 12345);
            ans = Math.min(ans, cntLeft + cntRight);
        }

        bw.write(ans + "\n");

        bw.close();
    }

    public static void bck(int pos, int tar, int cnt, long status) {
        if(pos == tar) {
            results.add(new long[]{status,cnt});
            return;
        }
        bck(pos+1, tar, cnt, status);
        bck(pos+1, tar, cnt+1, status ^ toggle[pos]);
    }

}
```
