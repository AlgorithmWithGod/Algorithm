```java
import java.io.*;
import java.util.*;

public class Main {
    static int n;
    static int[] str, weight;
    static int answer = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        str = new int[n];
        weight = new int[n];

        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            str[i] = Integer.parseInt(st.nextToken());
            weight[i] = Integer.parseInt(st.nextToken());
        }

        dfs(0);
        System.out.println(answer);
    }

    static void dfs(int idx) {
        if (idx == n) {
            int broken = 0;
            for (int i = 0; i < n; i++) {
                if (str[i] <= 0) broken++;
            }
            answer = Math.max(answer, broken);
            return;
        }

        if (str[idx] <= 0) {
            dfs(idx + 1);
            return;
        }

        boolean hit = false;

        for (int i = 0; i < n; i++) {
            if (i == idx || str[i] <= 0) continue;

            hit = true;

            str[idx] -= weight[i];
            str[i] -= weight[idx];

            dfs(idx + 1);

            str[idx] += weight[i];
            str[i] += weight[idx];
        }

        if (!hit) dfs(idx + 1);
    }
}
```
