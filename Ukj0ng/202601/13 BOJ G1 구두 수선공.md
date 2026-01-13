```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static PriorityQueue<Task> pq;
    private static int[][] task;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();

        while (!pq.isEmpty()) {
            bw.write(pq.poll().index + " ");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        task = new int[N+1][2];

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            task[i][0] = Integer.parseInt(st.nextToken());
            task[i][1] = Integer.parseInt(st.nextToken());
        }

        pq = new PriorityQueue<>((o1, o2) -> {
            if (o1.val != o2.val) return Double.compare(o2.val, o1.val);
            return Integer.compare(o1.index, o2.index);
        });

        for (int i = 1; i <= N; i++) {
            pq.add(new Task(i, (double)task[i][1]/task[i][0], task[i][0]));
        }
    }

    static class Task {
        int index;
        double val;
        int time;

        public Task(int index, double val, int time) {
            this.index = index;
            this.val = val;
            this.time = time;
        }
    }
}
```
