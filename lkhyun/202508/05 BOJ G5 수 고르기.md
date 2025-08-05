```java
import java.util.*;
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    static StringTokenizer st;
    static int N,M;
    static int[] A;

    public static void main(String[] args) throws Exception {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        A = new int[N];

        for (int i = 0; i < N; i++) {
            A[i] = Integer.parseInt(br.readLine());
        }
        Arrays.sort(A);

        int ans = Integer.MAX_VALUE;
        int left = 0, right = 0;
        
        while (right < N && left < N) {
            int d = A[right] - A[left];
            
            if (d >= M) {
                ans = Math.min(ans, d);
                left++;
            } else {
                right++;
            }
        }
        bw.write(ans+"");
        bw.close();
    }
}
```
