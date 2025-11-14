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

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            events.add(new int[]{Integer.parseInt(st.nextToken()), 0});
            events.add(new int[]{Integer.parseInt(st.nextToken()), 1});
        }

        events.sort((o1, o2) -> {
            if (o1[0] == o2[0]) return Integer.compare(o2[1], o1[1]);
            return Integer.compare(o1[0], o2[0]);
        });
    }

    private static int sweeping() {
        int result = 0;
        int count = 0;

        for (int[] event : events) {
            if (event[1] == 0) count++;
            else count--;

            result = Math.max(result, count);
        }

        return result;
    }
}
```
