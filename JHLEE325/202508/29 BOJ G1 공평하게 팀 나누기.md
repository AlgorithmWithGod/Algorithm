```java
import java.io.*;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];
        int weight_sum = 0;

        for (int i = 0; i < n; i++) {
            arr[i] = Integer.parseInt(br.readLine());
            weight_sum += arr[i];
        }

        int member = n / 2;

        boolean[][] weight = new boolean[member + 1][weight_sum + 1];

        weight[0][0] = true;

        for (int w : arr) {
            for (int i = member; i >= 1; i--) {
                for (int ws = weight_sum; ws >= 0; ws--) {
                    if (weight[i - 1][ws])
                        weight[i][ws + w] = true;
                }
            }
        }

        int big = 0, small = 0;
        int difference = 987654321;

        for (int i = 0; i <= weight_sum; i++) {
            if (weight[member][i]) {
                int difftemp = Math.abs(weight_sum - (i * 2));
                if (difftemp < difference) {
                    difference = difftemp;
                    big = Math.max(weight_sum - i, i);
                    small = Math.min(weight_sum - i, i);
                }
            }
        }

        System.out.println(small + " " + big);

    }
}

```
