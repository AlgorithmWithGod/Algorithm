```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();
        
        int n = Integer.parseInt(br.readLine());
        int[][] matrix = new int[n + 1][n + 1];
        
        for (int i = 1; i <= n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int j = 1; j <= n; j++) {
                matrix[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        
        int q = Integer.parseInt(br.readLine());
        
        for (int i = 0; i < q; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int x1 = Integer.parseInt(st.nextToken());
            int y1 = Integer.parseInt(st.nextToken());
            int x2 = Integer.parseInt(st.nextToken());
            int y2 = Integer.parseInt(st.nextToken());
            
            Set<Integer> distinctNumbers = new HashSet<>();
            
            for (int x = x1; x <= x2; x++) {
                for (int y = y1; y <= y2; y++) {
                    distinctNumbers.add(matrix[x][y]);
                }
            }
            
            sb.append(distinctNumbers.size()).append('\n');
        }
        
        System.out.print(sb);
    }
}
```
