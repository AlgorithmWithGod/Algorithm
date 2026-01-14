```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int MOD = 40000;
    private static PriorityQueue<Task> pq;
    private static int N;
    private static long t;

    public static void main(String[] args) throws IOException {
        init();

        while (!pq.isEmpty()) {
            Task temp = pq.poll();
            t += temp.a*t+temp.b;
            t %= MOD;
        }

        bw.write(t + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        pq = new PriorityQueue<>((o1, o2) -> {
            if (o1.a == 0 && o2.a == 0) return 0;
            if (o1.a == 0) return 1;
            if (o2.a == 0) return -1;
            return Long.compare(o2.a*o1.b, o1.a*o2.b);
        });

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            pq.add(new Task(Long.parseLong(st.nextToken()), Long.parseLong(st.nextToken())));
        }
    }

    static class Task {
        long a;
        long b;

        public Task(long a, long b) {
            this.a = a;
            this.b = b;
        }
    }
}
```
