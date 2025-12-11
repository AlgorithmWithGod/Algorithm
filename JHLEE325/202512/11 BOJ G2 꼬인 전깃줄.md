```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int N = Integer.parseInt(br.readLine());
        int[] arr = new int[N];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        int[] lis = new int[N];
        int len = 0;

        for (int x : arr) {
            int pos = Arrays.binarySearch(lis, 0, len, x);
            if (pos < 0) pos = -(pos + 1);

            lis[pos] = x;
            if (pos == len) len++;
        }

        System.out.println(N - len);
    }
}
```
