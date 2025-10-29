```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_16938_캠프_준비 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int N, L, R, X, ans;
    private static int[] questions, selected;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        X = Integer.parseInt(st.nextToken());
        ans = 0;

        st = new StringTokenizer(br.readLine());
        questions = new int[N];
        for (int i = 0; i < N; i++) {
            questions[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(questions);

        selected = new int[N];
    }

    private static void sol() throws IOException {
        dfs(0, 0);

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void dfs(int depth, int start) throws IOException {
        if (2 <= depth && depth <= N) {
            if (checkValid(depth)) {
                ans++;
            }
        }

        if (depth == N) {
            return;
        }

        for (int i = start; i < N; i++) {
            selected[depth] = i;
            dfs(depth + 1, i + 1);
        }
    }

    private static boolean checkValid(int depth) throws IOException {
        int sum = 0;

        for (int i = 0; i < depth; i++) {
            sum += questions[selected[i]];
        }

        return L <= sum && sum <= R && questions[selected[depth - 1]] - questions[selected[0]] >= X;
    }

}
```