```java
import java.io.*;
import java.util.*;

public class Main {
    
    static long[][] dp = new long[31][31];

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder sb = new StringBuilder();

        while (true) {
            int n = Integer.parseInt(br.readLine());
            if (n == 0) {
                break;
            }
            sb.append(countPills(n, 0)).append("\n");
        }
        System.out.print(sb);
    }
    
    static long countPills(int w, int h) {
        if (dp[w][h] != 0) {
            return dp[w][h];
        }
        
        if (w == 0) {
            return 1;
        }

        long result = countPills(w - 1, h + 1);
        
        if (h > 0) {
            result += countPills(w, h - 1);
        }

        dp[w][h] = result;
        return result;
    }
}
```
