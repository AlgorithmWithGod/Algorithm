```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[][] map;
    private static int[][][] sum;
    private static int N, Q;
    public static void main(String[] args) throws IOException {
        init();

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        map = new int[N+1][N+1];
        sum = new int[N+1][N+1][11];

        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int i = 1; i <= N; i++) {
            for (int j = 1; j <= N; j++) {
                for (int k = 1; k <= 10; k++) {
                    sum[i][j][k] += sum[i-1][j][k] + sum[i][j-1][k] - sum[i-1][j-1][k];
                }
                sum[i][j][map[i][j]]++;
            }
        }

        Q = Integer.parseInt(br.readLine());
        int[] temp = new int[11];

        while (Q-->0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int y1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());
            int count = 0;

            Arrays.fill(temp, 0);
            for (int i = 1; i <= 10; i++) {
                temp[i] += sum[x2][y2][i] - sum[x1-1][y2][i] - sum[x2][y1-1][i] + sum[x1-1][y1-1][i];
                if (temp[i] > 0) count++;
            }

            bw.write(count + "\n");
        }
    }
}
```
