```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<int[]> events;
    private static int[][] points, traffic;
    private static int N, M;
    public static void main(String[] args) throws IOException {
        init();
        long answer = sweep();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        events = new ArrayList<>();
        points = new int[N+1][2];
        traffic = new int[M][3];

        for (int i = 1; i <= N; i++) {
            st = new StringTokenizer(br.readLine());
            points[i][0] = Integer.parseInt(st.nextToken());
            points[i][1] = Integer.parseInt(st.nextToken());
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            traffic[i][0] = Math.min(points[u][1], points[v][1]);
            traffic[i][1] = Math.max(points[u][1], points[v][1]);
            traffic[i][2] = c;
        }

        Arrays.sort(traffic, (o1, o2) -> {
            if (o1[0] == o2[0]) return Integer.compare(o1[1], o2[1]);
            return Integer.compare(o1[0], o2[0]);
        });

        for (int[] t : traffic) {
            events.add(new int[]{t[0], t[2], 1});
            events.add(new int[]{t[1]+1, t[2], -1});
        }

        events.sort((o1, o2) -> {
            if (o1[0] != o2[0]) return Integer.compare(o1[0], o2[0]);
            return Integer.compare(o1[2], o2[2]);
        });
    }

    private static long sweep() {
        long result = 0;
        long current= 0;

        for (int[] e : events) {
            current += (long)e[1]*e[2];
            result = Math.max(result, current);
        }

        return result;
    }
}
```
