```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<int[]> events;
    private static int N;
    public static void main(String[] args) throws IOException {
        init();

        int answer = sweeping();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        events = new ArrayList<>();
        while (N-->0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            events.add(new int[]{x, y});
        }

        events.sort((o1, o2) -> {
            if (o1[0] == o2[0]) return Integer.compare(o2[1], o1[1]);
            return Integer.compare(o1[0], o2[0]);
        });
    }

    private static int sweeping() {
        int length = 0;
        int start = -2000000000;
        int end = -2000000000;

        for (int[] event : events) {
            if (end < event[0]) {
                length += end-start;
                start = event[0];
                end = event[1];
            } else {
                end = Math.max(end, event[1]);
            }
        }

        length += end-start;

        return length;
    }
}
```
