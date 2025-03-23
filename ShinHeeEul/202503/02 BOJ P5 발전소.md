```java
import java.io.*;
import java.util.*;

public class Main {

    static int[][] arr;
    static int[] dp;
    static int N;
    static int P;
    static final int DEFAULT = Integer.MAX_VALUE >> 1;
    static int min = DEFAULT;

    public static void main(String[] args) throws Exception {
        N = read();

        arr = new int[N][N];
        dp = new int[(1 << N)];

        Arrays.fill(dp, DEFAULT);

        int start = 0;
        for(int i = 0; i < N; i++) {
            for(int j = 0; j < N; j++) {
                arr[i][j] = read();
            }
        }
        for(int i = 0; i < N; i++) {
            if(System.in.read() == 'Y') {
                start |= (1 << i);
            }
        }
        System.in.read();
        P = read();
        dp[start] = 0;

        for(int i = start; i < (1 << N); i++) {

            // 갯수 세기
            int cnt = 0;

            // 들어가는 거
            for(int j = 0; j < N; j++) {
                // 나가는 거
                if(((1 << j) | i) != i) continue;
                cnt++;
                for(int a = 0; a < N; a++) {
                    int ll = ((1 << a) | i);
                    if(ll == i) continue;
                    dp[ll] = Math.min(dp[ll], dp[i] + arr[j][a]);
                }
            }

            if(cnt >= P) min = Math.min(dp[i], min);

        }

        System.out.println(min == DEFAULT ? -1 : min);
    }


    private static int read() throws Exception {
        int d, o;
        d = System.in.read();

        o = d & 15;

        while ((d = System.in.read()) > 32)
            o = (o << 3) + (o << 1) + (d & 15);

        return o;
    }

}
```
