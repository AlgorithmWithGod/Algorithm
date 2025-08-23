```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static boolean[] used;
    private static int N, M, answer;

    public static void main(String[] args) throws IOException {
        init();

        for (int i = 0; i <= 1000000; i++) {
            if (canPush(i)) {
                int n = Math.abs(N - i) + length(i);
                answer = Math.min(answer, n);
            }
        }

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        M = Integer.parseInt(br.readLine());
        answer = Math.abs(N - 100);

        used = new boolean[10];
        Arrays.fill(used, true);

        if (M > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());

            for (int i = 0; i < M; i++) {
                int n = Integer.parseInt(st.nextToken());
                used[n] = false;
            }
        }
    }

    private static boolean canPush(int num) {
        if (num == 0) return used[num];

        while (num > 0) {
            int n = num % 10;
            if (!used[n]) return false;
            num /= 10;
        }

        return true;
    }

    private static int length(int num) {
        if (num == 0) return 1;

        int count = 0;
        while (num > 0) {
            count++;
            num /= 10;
        }

        return count;
    }
}
```
