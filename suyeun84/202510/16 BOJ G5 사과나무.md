```java
import java.io.*;
import java.util.*;

public class boj20002 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static void nextLine() throws Exception { st = new StringTokenizer(br.readLine()); }
    static int nextInt() { return Integer.parseInt(st.nextToken()); }

    public static void main(String[] args) throws Exception {
        nextLine();
        int N = nextInt();
        int[][] arr = new int[N+1][N+1];
        int answer = -1000*300*300-1;
        for (int i = 1; i <= N; i++) {
            nextLine();
            for (int j = 1; j <= N; j++) {
                int tmp = nextInt();
                arr[i][j] = tmp + arr[i-1][j] + arr[i][j-1] - arr[i-1][j-1];
            }
        }
        for (int k = 1; k <= N; k++) {
            for (int i = k; i <= N; i++) {
                for (int j = k; j <= N; j++) {
                    answer = Math.max(answer, arr[i][j] - arr[i][j-k] - arr[i-k][j] + arr[i-k][j-k]);
                }
            }
        }
        System.out.println(answer);
    }
}
```
