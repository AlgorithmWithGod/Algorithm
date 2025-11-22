```java
import java.io.*;
import java.util.ArrayDeque;
import java.util.StringTokenizer;

public class BJ_11003_최솟값_찻기 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, L;
    private static int[]            nums;
    private static ArrayDeque<Node> dq;

    private static class Node {

        int idx;
        int val;

        Node(int idx, int val) {
            this.idx = idx;
            this.val = val;
        }

    }

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());

        nums = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            nums[i] = Integer.parseInt(st.nextToken());
        }
        dq = new ArrayDeque<>();
    }

    private static void sol() throws IOException {
        for (int i = 0; i < N; i++) {
            while (!dq.isEmpty() && dq.getLast().val >= nums[i]) dq.removeLast();

            dq.addLast(new Node(i, nums[i]));

            if (dq.getFirst().idx <= i - L) dq.removeFirst();

            bw.write(Integer.toString(dq.getFirst().val));
            bw.write(' ');
        }

        bw.flush();
        bw.close();
        br.close();
    }

}
```