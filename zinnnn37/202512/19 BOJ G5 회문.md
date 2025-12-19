```java
import java.io.*;

public class BJ_17609_회문 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static final StringBuilder  sb = new StringBuilder();

    private static int    N;
    private static String input;

    public static void main(String[] args) throws IOException {
        N = Integer.parseInt(br.readLine());

        while (N-- > 0) {
            input = br.readLine();
            sb.append(sol(0, input.length() - 1, 0)).append("\n");
        }
        bw.write(sb.toString());
        bw.flush();
        br.close();
        bw.close();
    }

    private static int sol(int left, int right, int cnt) {
        if (cnt >= 2) {
            return 2;
        }

        while (left < right) {
            if (input.charAt(left) == input.charAt(right)) {
                left++;
                right--;
            } else {
                return Math.min(sol(left + 1, right, cnt + 1), sol(left, right - 1, cnt + 1));
            }
        }
        return cnt;
    }

}
```