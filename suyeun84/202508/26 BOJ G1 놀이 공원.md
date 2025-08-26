```java
import java.util.*;
import java.io.*;

public class boj1561 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static long N;
    static int M, max = 0;
    static int[] time;
    public static void main(String[] args) throws Exception {
        nextLine();
        N = nextInt();
        M = nextInt();
        time = new int[M+1];
        nextLine();
        for (int i = 1; i <= M; i++) {
            time[i] = nextInt();
            max = Math.max(max, time[i]);
        }
        if (N <= M) {
            System.out.println(N);
            return;
        } else {
            long t = search();

            long cnt = M;
            for (int i = 1; i <= M; i++)
                cnt += (t - 1) / time[i];

            for (int i = 1; i <= M; i++) {

                if (t % time[i] == 0)
                    cnt++;

                if (cnt == N) {
                    System.out.println(i);
                    return;
                }
            }
        }
    }
    static long search() {
        long start = 0;
        long end = N/M * max;
        while (start <= end) {
            long mid = (start + end) / 2;
            long sum = M;
            for (int i = 1; i <= M; i++) sum += mid / time[i];
            if (sum < N) start = mid + 1;
            else end = mid - 1;
        }
        return start;
    }
}
```
