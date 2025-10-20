```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] lines;
    private static int N;
    public static void main(String[] args) throws IOException {
        init();
        int answer = sweep();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        lines = new int[N][2];

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            lines[i][0] = Integer.parseInt(st.nextToken());
            lines[i][1] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(lines, (o1, o2) -> {
            if (o1[0] == o2[0]) return Integer.compare(o1[1], o2[1]);
            return Integer.compare(o1[0], o2[0]);
        });
    }

    private static int sweep() {
        int result = 0;
        int prevS = -1000000001;
        int prevE = -1000000001;

        for (int[] line : lines) {
            if (prevE < line[0]) {
                result += (prevE - prevS);
                prevS = line[0];
            }

            prevE = Math.max(prevE, line[1]);
        }

        result += (prevE - prevS);
        return result;
    }
}
```
