```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception {st = new StringTokenizer(br.readLine());}
    static int nextInt() {return Integer.parseInt(st.nextToken());}

    static int n, m, r, answer = 0;
    static int[] item;
    static int[][] dist;
    public static void main(String[] args) throws Exception {
        nextLine();
        n = nextInt();
        m = nextInt();
        r = nextInt();
        item = new int[n+1];
        dist = new int[n+1][n+1];
        for (int i = 1; i <= n; i++) {
            Arrays.fill(dist[i], 16);
            dist[i][i] = 0;
        }
        nextLine();
        for (int i = 1; i <= n; i++) item[i] = nextInt();
        for (int i = 0; i < r; i++) {
            nextLine();
            int a = nextInt();
            int b = nextInt();
            int l = nextInt();
            dist[a][b] = l;
            dist[b][a] = l;
        }

        floyd();
        System.out.println(answer);
    }

    static void floyd() {
        for (int k = 1; k <= n; k++) {
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= n; j++) {
                    if (dist[i][j] > dist[i][k] + dist[k][j]) {
                        dist[i][j] = dist[i][k] + dist[k][j];
                    }
                }
            }
        }
        solve();
    }

    static void solve() {
        for (int i = 1; i <= n; i++) {
            int sum = 0;
            for (int j = 1; j <= n; j++) {
                if (dist[i][j] <= m) sum += item[j];
            }
            answer = Math.max(answer, sum);
        }
    }
}
```
