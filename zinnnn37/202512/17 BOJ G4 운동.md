```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_1956_운동 {

    private static final int INF = 987654321;

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int V, E, ans;
    private static int[][] matrix;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());
        ans = INF;

        matrix = new int[V + 1][V + 1];
        for (int i = 1; i <= V; i++) {
            Arrays.fill(matrix[i], INF);
        }

        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());

            matrix[a][b] = w;
        }

    }

    private static void sol() throws IOException {
        for (int k = 1; k <= V; k++) {
            for (int i = 1; i <= V; i++) {
                for (int j = 1; j <= V; j++) {
                    matrix[i][j] = Math.min(matrix[i][j], matrix[i][k] + matrix[k][j]);
                }
            }
        }

        for (int i = 1; i <= V; i++) {
            ans = Math.min(ans, matrix[i][i]);
        }

        bw.write(ans != INF ? ans + "" : "-1");

        bw.flush();
        bw.close();
        br.close();
    }

}
```