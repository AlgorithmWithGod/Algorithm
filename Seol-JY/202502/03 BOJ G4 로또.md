```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        long[][] arr = new long[101][2_001];
        
        for (long i = 1; i < 2_001; i++) {
            arr[1][(int)i] = i;
        }
        
        for (long i = 2; i < 101; i++) {
            for (long j = 1; j < 2_001; j++) {
                arr[(int)i][(int)j] = arr[(int)i][(int)(j-1)] + arr[(int)(i-1)][(int)(j/2)];
            }
        }
        
        long T = Long.parseLong(br.readLine());
        
        for (long i = 0; i < T; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            long n = Long.parseLong(st.nextToken());
            long m = Long.parseLong(st.nextToken());
            System.out.println(arr[(int)n][(int)m]);
        }
    }
}
```
