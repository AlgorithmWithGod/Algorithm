```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static List<Long>[] dimensions;
    private static long[] median;
    private static long dist;
    private static int N, M;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(dist + "\n");
        for (long temp : median) {
            bw.write(temp + " ");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        dimensions = new List[N];
        median = new long[N];
        for (int i = 0; i < N; i++) {
            dimensions[i] = new ArrayList<>();
        }

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            for (int j = 0; j < N; j++) {
                long input = Long.parseLong(st.nextToken());
                dimensions[j].add(input);
            }
        }

        for (List<Long> dimension : dimensions) {
            Collections.sort(dimension);
        }

        for (int i = 0; i < N; i++) {
            median[i] = dimensions[i].get(M/2);
            for (long temp : dimensions[i]) {
                dist += Math.abs(median[i]-temp);
            }
        }
    }
}
```
