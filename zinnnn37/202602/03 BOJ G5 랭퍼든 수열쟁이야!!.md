```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_15918_랭퍼든_수열쟁이야 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int n, x, y, fixed, ans;
    private static int[] arr;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        x = Integer.parseInt(st.nextToken()) - 1;
        y = Integer.parseInt(st.nextToken()) - 1;

        arr = new int[2 * n];
        fixed = y - x - 1;
        arr[x] = arr[y] = fixed;
    }

    private static void sol() throws IOException {
        rec(n);
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void rec(int num) {
        if (num < 1) {
            ans++;
            return;
        }

        if (num == fixed) {
            rec(num - 1);
            return;
        }

        for (int idx = 0; idx < 2 * n; idx++) {
            if (idx + num + 1 >= 2 * n || arr[idx] != 0 || arr[idx + num + 1] != 0) {
                continue;
            }
            arr[idx] = arr[idx + num + 1] = num;
            rec(num - 1);
            arr[idx] = arr[idx + num + 1] = 0;
        }
    }

}
```