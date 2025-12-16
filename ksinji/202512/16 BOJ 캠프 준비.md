```java
import java.io.*;
import java.util.*;

public class Main {
    static int n, l, r, y;
    static int[] a;
    static int ans = 0;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        l = Integer.parseInt(st.nextToken());
        r = Integer.parseInt(st.nextToken());
        y = Integer.parseInt(st.nextToken());

        a = new int[n];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) a[i] = Integer.parseInt(st.nextToken());

        dfs(0, 0, 0, 0, 0);
        System.out.println(ans);
    }
    
    static void dfs(int idx, int cnt, int sum, int mn, int mx) {
        if (sum > r) return;

        if (idx == n) {
            if (cnt >= 2 && sum >= l && sum <= r && (mx - mn) >= y) ans++;
            return;
        }

        dfs(idx + 1, cnt, sum, mn, mx);

        int v = a[idx];
        if (cnt == 0) {
            dfs(idx + 1, 1, sum + v, v, v);
        } else {
            dfs(idx + 1, cnt + 1, sum + v, Math.min(mn, v), Math.max(mx, v));
        }
    }
}
```
