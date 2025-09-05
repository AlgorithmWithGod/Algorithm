```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
    private static BufferedReader br;
    private static int N;
    private static int[] X;
    private static int[] answer;
    private static boolean[] used;
    private static boolean found;

    public static void main(String[] args) throws IOException {
        br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        X = new int[N];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            X[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(X);
        answer = new int[2 * N];
        Arrays.fill(answer, -1);
        used = new boolean[N];

        backtrack(0);

        if (!found) {
            System.out.println(-1);
        }
    }

    private static void backtrack(int idx) {
        if (found)
            return;


        if (idx == 2 * N) {
            StringBuilder sb = new StringBuilder();
            for (int v : answer) sb.append(v).append(' ');
            System.out.println(sb.toString());
            found = true;
            return;
        }
        if (answer[idx] != -1) {
            backtrack(idx + 1);
            return;
        }

        for (int i = 0; i < N; i++) {
            if (used[i])
                continue;
            int val = X[i];
            int secIdx = idx + val + 1;
            if (secIdx >= 2 * N || answer[secIdx] != -1) continue;

            answer[idx] = val;
            answer[secIdx] = val;
            used[i] = true;

            backtrack(idx + 1);

            answer[idx] = -1;
            answer[secIdx] = -1;
            used[i] = false;
        }
    }
}
```
