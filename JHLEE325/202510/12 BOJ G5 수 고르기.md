```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());

        int[] arr = new int[n];

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }

        Arrays.sort(arr);

        int left = 0;
        int right = 0;
        int ans = Integer.MAX_VALUE;

        while (right < n) {
            int diff = arr[right] - arr[left];

            if (diff < m) {
                right++;
                continue;
            }
            if (diff == m) {
                ans = m;
                break;
            }
            ans = Math.min(ans, diff);
            left++;

        }

        System.out.println(ans);
    }
}
```
