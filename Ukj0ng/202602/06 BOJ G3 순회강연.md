```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final int INF = 10000;
    private static PriorityQueue<College> pq;
    private static long[] arr;
    private static long answer;
    private static int N;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        pq = new PriorityQueue<>((o1, o2) -> Double.compare(o2.cost, o1.cost));
        arr = new long[INF+1];

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int p = Integer.parseInt(st.nextToken());
            int d = Integer.parseInt(st.nextToken());

            pq.add(new College(d, p));
        }

        while (!pq.isEmpty()) {
            College current = pq.poll();

            for (int i = current.day; i > 0; i--) {
                if (arr[i] < current.cost) {
                    arr[i] = current.cost;
                    break;
                }
            }
        }

        for (int i = 1; i <= INF; i++) {
            answer += arr[i];
        }
    }

    static class College {
        int day;
        int cost;

        College (int day, int cost) {
            this.day = day;
            this.cost = cost;
        }
    }
}
```
