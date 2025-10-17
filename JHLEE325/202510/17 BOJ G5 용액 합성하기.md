```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());

        int[] arr = new int[n];

        st = new StringTokenizer(br.readLine());

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        int left = 0;
        int right = n - 1;
        int temp = 987654321;
        int res = 0;

        while (left < right) {
            int sum = arr[left] + arr[right];
            if (sum < 0) {
                left++;
            } else if (sum > 0) {
                right--;
            } else {
                res = 0;
                break;
            }
            if(temp> Math.abs(sum)){
                res = sum;
                temp = Math.abs(sum);
            }
        }

        System.out.println(res);
    }
}
```
