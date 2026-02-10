```java
import java.io.*;
import java.util.Arrays;

public class BJ_3649_로봇_프로젝트 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder  sb = new StringBuilder();

    private static int x, n;
    private static String line;
    private static int[]  lego;

    public static void main(String[] args) throws IOException {
        while ((line = br.readLine()) != null && !line.trim().isEmpty()) {
            init();
            sol();
        }

        bw.write(sb.toString());
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        x = Integer.parseInt(line.trim()) * 10_000_000;
        n = Integer.parseInt(br.readLine());

        lego = new int[n];
        for (int i = 0; i < n; i++) {
            lego[i] = Integer.parseInt(br.readLine());
        }
        Arrays.sort(lego);
    }

    private static void sol() throws IOException {
        int left  = 0;
        int right = n - 1;

        while (left < right) {
            int sum = lego[left] + lego[right];

            if (sum == x) {
                sb.append("yes ").append(lego[left]).append(" ").append(lego[right]).append("\n");
                return;
            } else if (sum < x) {
                left++;
            } else {
                right--;
            }
        }
        sb.append("danger\n");
    }

}
```