```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder sb = new StringBuilder();
    private static Stack<Integer> stack;
    private static int N, K, count;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(sb.toString() + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(st.nextToken());

        stack = new Stack<>();
        char[] input = br.readLine().toCharArray();

        int i = 0;

        while (i < N) {
            int n = input[i] - '0';

            while (count < K && (!stack.isEmpty() && stack.peek() < n)) {
                stack.pop();
                count++;
            }
            stack.push(n);
            i++;
        }

        while (count < K) {
            stack.pop();
            count++;
        }

        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }

        sb.reverse();
    }
}
```
