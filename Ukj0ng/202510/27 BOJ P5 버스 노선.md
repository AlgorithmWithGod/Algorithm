```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<int[]> busLines;
    private static boolean[] contains;
    private static int N, M;
    public static void main(String[] args) throws IOException {
        init();
        sweep();

        for (int i = 1; i <= M; i++) {
            if (!contains[i]) bw.write(i + " ");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        M = Integer.parseInt(br.readLine());

        busLines = new ArrayList<>();
        contains = new boolean[M+1];

        for (int i = 1; i <= M; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            if (a < b) {
                busLines.add(new int[]{a, b, i});
                busLines.add(new int[]{a+N, b+N, i});
            } else {
                busLines.add(new int[]{a, b+N, i});
            }
        }

        busLines.sort((o1, o2) -> {
            if (o1[0] == o2[0]) return Integer.compare(o2[1], o1[1]);
            return Integer.compare(o1[0], o2[0]);
        });
    }

    private static void sweep() {
        int end = -1;

        for (int[] busLine : busLines) {
            if (busLine[1] <= end) {
                contains[busLine[2]] = true;
            } else {
                end = busLine[1];
            }
        }
    }
}
```
