```
import java.io.*;
import java.util.Objects;
import java.util.StringTokenizer;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static Node[] history;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            char q = st.nextToken().charAt(0);

            if (q == 'a') {
                int val = Integer.parseInt(st.nextToken());
                history[i] = new Node(val, history[i-1]);
            } else if (q == 's') {
                history[i] = history[i-1].prev;
            } else {
                int time = Integer.parseInt(st.nextToken());
                history[i] = history[time-1];
            }

            if (Objects.isNull(history[i])) bw.write("-1" + "\n");
            else bw.write(history[i].val + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        history = new Node[N + 1];

        history[0] = null;
    }

    static class Node {
        int val;
        Node prev;

        public Node(int val, Node prev) {
            this.val = val;
            this.prev = prev;
        }
    }
}
```
