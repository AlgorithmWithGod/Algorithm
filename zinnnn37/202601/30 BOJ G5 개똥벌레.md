```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_3020_개똥벌레 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, H;
    private static int[] stalactite, stalagmite, prefix1, prefix2;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        H = Integer.parseInt(st.nextToken());

        stalactite = new int[H + 2];
        stalagmite = new int[H + 2];
        for (int i = 0; i < N / 2; i++) {
            stalagmite[Integer.parseInt(br.readLine())] += 1;
            stalactite[H - Integer.parseInt(br.readLine()) + 1] += 1;
        }

        prefix1 = new int[H + 2];
        for (int i = 1; i <= H; i++) {
            prefix1[i] += prefix1[i - 1] + stalactite[i];
        }

        prefix2 = new int[H + 2];
        for (int i = H; i > 0; i--) {
            prefix2[i] += prefix2[i + 1] + stalagmite[i];
        }
    }

    private static void sol() throws IOException {
        int cnt = 0;
        int sum = 0;
        int min = Integer.MAX_VALUE;
        for (int i = 1; i <= H; i++) {
            sum = prefix1[i] + prefix2[i];

            if (sum == min) {
                cnt++;
            }
            if (sum < min) {
                min = sum;
                cnt = 1;
            }
        }
        bw.write(min + " " + cnt);
        bw.flush();
        bw.close();
        br.close();
    }

}
```
