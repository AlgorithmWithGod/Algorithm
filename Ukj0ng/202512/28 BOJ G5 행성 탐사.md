```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static char[][] map;
    private static int[][] sumJ, sumO, sumI;
    private static int M, N, K;

    public static void main(String[] args) throws IOException {
        init();

        while (K-->0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());
            int d = Integer.parseInt(st.nextToken());

            bw.write(count(sumJ, a, b, c, d) + " " + count(sumO, a, b, c, d) + " " + count(sumI, a, b, c, d) + "\n");
        }
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        StringTokenizer st = new StringTokenizer(br.readLine());
        M = Integer.parseInt(st.nextToken());
        N = Integer.parseInt(st.nextToken());
        K = Integer.parseInt(br.readLine());

        map = new char[M+1][N+1];
        sumJ = new int[M+1][N+1];
        sumO = new int[M+1][N+1];
        sumI = new int[M+1][N+1];

        for (int i = 1; i <= M; i++) {
            char[] input = br.readLine().toCharArray();
            for (int j = 1; j <= N; j++) {
                map[i][j] = input[j-1];
            }
        }

        for (int i = 1; i <= M; i++) {
            for (int j = 1; j <= N; j++) {
                sumJ[i][j] = sumJ[i-1][j] + sumJ[i][j-1] - sumJ[i-1][j-1];
                sumO[i][j] = sumO[i-1][j] + sumO[i][j-1] - sumO[i-1][j-1];
                sumI[i][j] = sumI[i-1][j] + sumI[i][j-1] - sumI[i-1][j-1];
                if (map[i][j] == 'J') {
                    sumJ[i][j]++;
                } else if (map[i][j] == 'O') {
                    sumO[i][j]++;
                } else {
                    sumI[i][j]++;
                }
            }
        }
    }

    private static int count(int[][] sum, int a, int b, int c, int d) {
        return sum[c][d] - sum[a-1][d] - sum[c][b-1] + sum[a-1][b-1];
    }
}
```
