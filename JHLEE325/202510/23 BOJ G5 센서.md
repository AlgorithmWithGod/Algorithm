```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n = Integer.parseInt(br.readLine());
        int k = Integer.parseInt(br.readLine());

        int[] sensors = new int[n];
        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < n; i++) {
            sensors[i] = Integer.parseInt(st.nextToken());
        }

        if (k >= n) {
            System.out.println(0);
            return;
        }

        Arrays.sort(sensors);

        int[] diff = new int[n - 1];
        for (int i = 0; i < n - 1; i++) {
            diff[i] = sensors[i + 1] - sensors[i];
        }

        Arrays.sort(diff);

        int sum = 0;
        for (int i = 0; i < n - k; i++) {
            sum += diff[i];
        }

        System.out.println(sum);
    }
}
```
