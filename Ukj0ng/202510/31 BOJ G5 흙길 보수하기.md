```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<int[]> events;
    private static int N, L, answer;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        L = Integer.parseInt(st.nextToken());
        answer = 0;
        int covered = -1;

        events = new ArrayList<>();

        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine());
            int start = Integer.parseInt(st.nextToken());
            int end = Integer.parseInt(st.nextToken());

            events.add(new int[]{start, end});
        }

        events.sort((o1, o2) -> Integer.compare(o1[1], o2[1]));

        for (int[] event : events) {
            if (covered < event[0]) {
                covered = event[0];
            }

            if (covered < event[1]) {
                int length = event[1] - covered;
                int temp = (length + L - 1) / L;
                covered += temp * L;
                answer += temp;
            }
        }
    }
}
```
