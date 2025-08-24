```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr, answer;
    private static Stack<Integer> stack;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();
        solve();

        for (int i = 0; i < N; i++) {
            if (answer[i] != -1) bw.write(answer[i] + "\n");
            else bw.write("infinity" + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        arr = new int[N];
        answer = new int[N];
        stack = new Stack<>();
        Arrays.fill(answer, -1);

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
    }

    private static void solve() {
        for (int i = 0; i < N; i++) {
            while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) {
                int idx = stack.pop();
                answer[idx] = i - idx;
            }
            stack.push(i);
        }
    }
}
```
