```java
import java.io.*;
import java.util.Arrays;

public class BJ_1339_단어_수학 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

    private static int N, ans;
    private static int[] cnt;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        cnt = new int[26];
        ans = 0;

        for (int i = 0; i < N; i++) {
            String input = br.readLine();

            int len = input.length();
            for (int j = 0; j < len; j++) {
                cnt[input.charAt(j) - 'A'] += (int) Math.pow(10, len - 1 - j);
            }
        }
        Arrays.sort(cnt);
    }

    private static void sol() throws IOException {
        int num = 9;

        for (int i = 25; i >= 0 && num > 0; i--) {
            ans += cnt[i] * num--;
        }

        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

}
```