```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_1074_Z {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, R, C, ans;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        C = Integer.parseInt(st.nextToken());
    }

    private static void sol() throws IOException {
        rec((int) Math.pow(2, N), R, C);
        
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void rec(int size, int r, int c) {
        if (size == 1) {
            return;
        }

        int half = size / 2;

        // 좌상
        if (r < half && c < half) {
            rec(half, r, c);
        }
        // 좌하
        else if (r < half) {
            ans += size * size / 4;
            rec(half, r, c - half);
        }
        // 우상
        else if (c < half) {
            ans += (size * size / 4) * 2;
            rec(half, r - half, c);
        }
        // 우하
        else {
            ans += (size * size / 4) * 3;
            rec(half, r - half, c - half);
        }
    }

}
```