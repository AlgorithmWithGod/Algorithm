```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Deque<Integer> deque = new ArrayDeque<>();
    private static int[][] towers;
    private static int[] dp, history;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(deque.size() + "\n");
        while (!deque.isEmpty()) {
            bw.write(deque.pollFirst() + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        towers = new int[N][4];
        dp = new int[N];
        history = new int[N];

        Arrays.fill(history, -1);

        int len = 0;
        int index = -1;

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            towers[i][0] = Integer.parseInt(st.nextToken());
            towers[i][1] = Integer.parseInt(st.nextToken());
            towers[i][2] = Integer.parseInt(st.nextToken());
            towers[i][3] = i + 1;
        }

        Arrays.sort(towers, (o1, o2) -> Integer.compare(o2[0], o1[0]));

        for (int i = 0; i < N; i++) {
            dp[i] = towers[i][1];

            for (int j = 0; j < i; j++) {
                if (towers[j][2] > towers[i][2]) {
                    if (dp[j] + towers[i][1] > dp[i]) {
                        dp[i] = dp[j] + towers[i][1];
                        history[i] = j;
                    }
                }
            }
            if (dp[i] > len) {
                len = dp[i];
                index = i;
            }
        }

        while (index != -1) {
            deque.addLast(towers[index][3]);
            index = history[index];
        }
    }
}
```
