```java
import java.util.*;
import java.io.*;

public class Main {

    static BufferedReader br;
    static BufferedWriter bw;
    static StringTokenizer st;

    static int N;
    static long[][] arr;

    public static void main(String[] args) throws Exception {
        bw = new BufferedWriter(new OutputStreamWriter(System.out));

        input();
        solve();

        bw.close();
    }

    public static void input() throws Exception {
        br = new BufferedReader(new InputStreamReader(System.in));

        N = Integer.parseInt(br.readLine());
        arr = new long[N][];
        for(int i=0;i<N;i++) {
            st = new StringTokenizer(br.readLine());
            arr[i] = new long[]{Long.parseLong(st.nextToken())/2, Long.parseLong(st.nextToken())/2};
        }

        br.close();
    }

    public static void solve() throws Exception {
        bw = new BufferedWriter(new OutputStreamWriter(System.out));

        Arrays.sort(arr, (a,b) -> {
            if(a[0] == b[0]) return Long.compare(a[1], b[1]);
            return Long.compare(b[0], a[0]);
        });
        long ans = 0, prev = 0;
        for(long[] point : arr) {
            long x = point[0], y = point[1];
            if(y > prev) {
                ans += (y-prev) * x;
                prev = y;
            }
        }
        bw.write((ans*4) + "\n");

        bw.close();
    }

}
```
