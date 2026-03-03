```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());

        int[] book = new int[N];
        
        st = new StringTokenizer(br.readLine());
        
        int maxDist = 0;
        for (int i = 0; i < N; i++) {
            book[i] = Integer.parseInt(st.nextToken());
            maxDist = Math.max(maxDist, Math.abs(book[i]));
        }

        Arrays.sort(book);

        long totalStep = 0;

        for (int i = 0; i < N && book[i] < 0; i += M) {
            totalStep += Math.abs(book[i]) * 2;
        }

        for (int i = N - 1; i >= 0 && book[i] > 0; i -= M) {
            totalStep += book[i] * 2;
        }

        System.out.println(totalStep - maxDist);
    }
}
```
