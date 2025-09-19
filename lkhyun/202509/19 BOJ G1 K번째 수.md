```java
import java.util.*;
import java.io.*;

public class Main{
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static StringBuilder sb = new StringBuilder();
    static long N,K;

    public static void main(String[] args) throws Exception {
        N = Integer.parseInt(br.readLine());
        K = Integer.parseInt(br.readLine());
        bw.write(binarySearch(1, N*N) +"");
        bw.close();
    }
    public static long binarySearch(long start, long end){
        long left = start;
        long right = end;
        long mid = 0;
        while (left <= right) {
            mid = (left + right) / 2;

            long smaller = 0;
            long equal = 0;
            
            for (int i = 1; i <= N; i++) {
                long maxJ = mid / i;
                
                if (maxJ > N) maxJ = N;
                
                if (mid % i == 0 && mid / i <= N) {
                    smaller += maxJ - 1;
                    equal++;
                } else {
                    smaller += maxJ;
                }
            }
            
            if (smaller >= K) {
                right = mid - 1;
            } else if (smaller + equal >= K) {
                return mid;
            } else {
                left = mid + 1;
            }
        }
        return mid;
    }
}
```
