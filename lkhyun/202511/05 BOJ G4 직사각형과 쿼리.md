```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringBuilder sb = new StringBuilder();
    static StringTokenizer st;
    public static void main(String[] args) throws Exception {
        int N = Integer.parseInt(br.readLine());
        int[][] mat = new int[N+1][N+1];
        
        for (int i = 1; i <= N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= N; j++) {
                mat[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        
        int[][][] sum = new int[11][N + 1][N + 1];
        
        for (int k = 1; k <= 10; k++) {
            for (int i = 1; i <= N; i++) {
                for (int j = 1; j <= N; j++) {
                    if(mat[i][j] == k) sum[k][i][j] = 1;
                    else sum[k][i][j] = 0;
                    
                    sum[k][i][j] += (sum[k][i-1][j] + sum[k][i][j-1] - sum[k][i-1][j-1]);
                }
            }
        }
        
        int Q = Integer.parseInt(br.readLine());
        
        for (int q = 0; q < Q; q++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int y1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());
            
            int count = 0;
            
            for (int k = 1; k <= 10; k++) {
                int result = sum[k][x2][y2] - sum[k][x1-1][y2] - sum[k][x2][y1-1] + sum[k][x1-1][y1-1];
                
                if (result > 0) count++;
            }
            
            bw.write(count + "\n");
        }
        bw.close();
    }
}
```
