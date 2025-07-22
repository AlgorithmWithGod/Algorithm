 ```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int n = Integer.parseInt(st.nextToken());
        int l = Integer.parseInt(st.nextToken());
        int r = Integer.parseInt(st.nextToken());
        int x = Integer.parseInt(st.nextToken());
        
        int[] a = new int[n];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            a[i] = Integer.parseInt(st.nextToken());
        }
        
        Arrays.sort(a);
        
        int answer = 0;
        
        for (int mask = 1; mask < (1 << n); mask++) {
            if (Integer.bitCount(mask) < 2) continue;
            
            int sum = 0;
            int min = Integer.MAX_VALUE;
            int max = Integer.MIN_VALUE;
            
            for (int i = 0; i < n; i++) {
                if ((mask & (1 << i)) != 0) {
                    sum += a[i];
                    min = Math.min(min, a[i]);
                    max = Math.max(max, a[i]);
                }
            }
            
            if (sum >= l && sum <= r && max - min >= x) {
                answer++;
            }
        }
        
        System.out.println(answer);
    }
}
```
