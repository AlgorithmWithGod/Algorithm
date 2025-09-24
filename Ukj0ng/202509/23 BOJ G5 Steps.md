```
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int T = Integer.parseInt(br.readLine());

        while (T-- > 0) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            long x = Long.parseLong(st.nextToken());
            long y = Long.parseLong(st.nextToken());
            long d = y - x;

            if (d == 0) {
                bw.write("0\n");
                continue;
            }

            long k = (long) Math.sqrt(d);

            while (k * k < d) k++;
            while (k * k > d) k--;

            if (k * k == d) {
                bw.write((2 * k - 1) + "\n");
            } else if (d <= k * k + k) {
                bw.write((2 * k) + "\n");
            } else {
                bw.write((2 * k + 1) + "\n");
            }
        }

        bw.flush();
        bw.close();
        br.close();
    }
}
```
