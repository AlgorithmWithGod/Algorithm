```java
import java.io.*;
import java.util.*;

public class Main {
    static double x, y, c;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        x = Double.parseDouble(st.nextToken());
        y = Double.parseDouble(st.nextToken());
        c = Double.parseDouble(st.nextToken());

        double left = 0.0;
        double right = Math.min(x, y);
        double ans = 0.0;

        for (int i = 0; i < 10000; i++) {
            double mid = (left + right) / 2.0;
            double h1 = Math.sqrt(x * x - mid * mid);
            double h2 = Math.sqrt(y * y - mid * mid);
            double tempc = (h1 * h2) / (h1 + h2);
            if (tempc >= c) {
                ans = mid;
                left = mid;
            } else {
                right = mid;
            }
        }

        System.out.printf("%.3f\n", ans);
    }
}
```
