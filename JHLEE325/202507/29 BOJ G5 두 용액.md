```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];

        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(arr);

        int left = 0;
        int right = n - 1;
        int temp = 2000000000;
        int l = 0, r = 0;

        while (left < right) {
            int x = arr[left];
            int y = arr[right];
            int sum = x + y;
            if (Math.abs(x + y) < Math.abs(temp)) {
                temp = sum;
                l = x;
                r = y;
            }
            if (sum > 0)
                right -= 1;
            else left += 1;
        }

        System.out.println(l + " " + r);
    }
}

```
