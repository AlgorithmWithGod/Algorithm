```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());

        int[] pgm = new int[n];

        st = new StringTokenizer(br.readLine());

        for (int i = 0; i < n; i++) {
            pgm[i] = Integer.parseInt(st.nextToken());
        }

        int left = 0;
        int right = n - 1;
        int res = 0;

        while (left < right) {
            res = Math.max((right - left - 1) * Math.min(pgm[left], pgm[right]), res);
            if (pgm[left] <= pgm[right]) {
                left++;
            } else {
                right--;
            }
        }

        System.out.println(res);
    }
}
```
