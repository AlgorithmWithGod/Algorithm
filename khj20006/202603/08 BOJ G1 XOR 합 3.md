```java
import java.io.*;
import java.util.*;

public class BOJ13710 {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        int[] arr = new int[N];
        for(int i=0;i<N;i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        long ans = 0;
        for(int k=0;k<30;k++) {
            long odd = 0, even = 1;
            int sum = 0;
            for(int i=0;i<N;i++) {
                int a = (arr[i] & (1 << k)) == 0 ? 0 : 1;
                sum ^= a;
                if(sum == 0) {
                    ans += odd * (1L << k);
                    even++;
                }
                else {
                    ans += even * (1L << k);
                    odd++;
                }
            }
        }
        bw.write(ans + "\n");
        bw.close();
    }

}
```
