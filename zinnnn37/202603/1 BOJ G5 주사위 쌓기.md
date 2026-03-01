```java
import java.io.*;
import java.util.StringTokenizer;

public class BJ_2116_주사위_쌓기 {

    private static final int[] pairs = new int[] { 5, 3, 4, 1, 2, 0 };

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, ans;
    private static int[][] dices, diceIdx;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        dices = new int[N][6];
        diceIdx = new int[N][7];
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < 6; j++) {
                dices[i][j] = Integer.parseInt(st.nextToken());
                diceIdx[i][dices[i][j]] = j;
            }
        }
    }

    private static void sol() throws IOException {
        findDice(0);

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void findDice(int num) {
        if (num == 6) {
            return;
        }

        int sum = 0;
        if (num == 0 || num == 5) {
            sum += findMax(0, 0, 5);
        } else if (num == 1 || num == 3) {
            sum += findMax(0, 1, 3);
        } else if (num == 2 || num == 4) {
            sum += findMax(0, 2, 4);
        }

        int prev = num;
        for (int i = 1; i < N; i++) {
            int cur = diceIdx[i][dices[i - 1][prev]];
            sum += findMax(i, cur, pairs[cur]);
            prev = pairs[cur];
        }

        ans = Math.max(ans, sum);

        findDice(num + 1);
    }

    private static int findMax(int idx, int up, int down) {
        int max = Math.max(dices[idx][up], dices[idx][down]);
        int min = Math.min(dices[idx][up], dices[idx][down]);

        if (max != 6) return 6;
        if (min != 5) {
            return 5;
        } else {
            return 4;
        }
    }

}
```