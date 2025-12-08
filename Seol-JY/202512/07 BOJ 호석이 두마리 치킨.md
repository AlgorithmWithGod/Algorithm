```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());
        
        int[][] dist = new int[n + 1][n + 1];
        int INF = 1000000;
        
        for (int i = 1; i <= n; i++) {
            Arrays.fill(dist[i], INF);
            dist[i][i] = 0;
        }
        
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            dist[a][b] = 1;
            dist[b][a] = 1;
        }
        
        for (int k = 1; k <= n; k++) {
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= n; j++) {
                    if (dist[i][j] > dist[i][k] + dist[k][j]) {
                        dist[i][j] = dist[i][k] + dist[k][j];
                    }
                }
            }
        }
        
        int ansI = 0, ansJ = 0, ansSum = Integer.MAX_VALUE;
        
        for (int i = 1; i <= n; i++) {
            for (int j = i + 1; j <= n; j++) {
                int sum = 0;
                for (int k = 1; k <= n; k++) {
                    sum += Math.min(dist[k][i], dist[k][j]) * 2;
                }
                if (sum < ansSum) {
                    ansSum = sum;
                    ansI = i;
                    ansJ = j;
                }
            }
        }
        
        System.out.println(ansI + " " + ansJ + " " + ansSum);
    }
}
```
