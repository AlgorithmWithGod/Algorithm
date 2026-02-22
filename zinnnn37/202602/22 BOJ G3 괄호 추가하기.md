```java
import java.io.*;

public class BJ_16637_괄호_추가하기 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    private static int N, ans;
    private static String line;
    private static int[]  nums;
    private static char[] ops;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        ans = Integer.MIN_VALUE;

        int numCnt = N / 2 + 1;
        nums = new int[numCnt];
        ops = new char[numCnt - 1];

        line = br.readLine();
        for (int i = 0; i < N; i++) {
            if (i % 2 == 0) {
                nums[i / 2] = line.charAt(i) - '0';
            } else {
                ops[i / 2] = line.charAt(i);
            }
        }
    }

    private static void sol() throws IOException {
        rec(0, nums[0]);

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void rec(int idx, int cur) {
        if (idx >= ops.length) {
            ans = Math.max(ans, cur);
            return;
        }

        int next      = nums[idx + 1];
        int noBracket = calc(cur, next, ops[idx]);
        rec(idx + 1, noBracket);

        if (idx + 1 < ops.length) {
            int bracketVal  = calc(next, nums[idx + 2], ops[idx + 1]);
            int withBracket = calc(cur, bracketVal, ops[idx]);
            rec(idx + 2, withBracket);
        }
    }

    private static int calc(int a, int b, char op) {
        if (op == '+') return a + b;
        if (op == '-') return a - b;
        return a * b;
    }

}
```