```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.StringTokenizer;

public class BJ_1806_부분합 {

    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static StringTokenizer st;

    private static int N;
    private static int S;
    private static int ans;
    private static int[] nums;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        st = new StringTokenizer(br.readLine());
        N = Integer.parseInt(st.nextToken());
        S = Integer.parseInt(st.nextToken());
        ans = Integer.MAX_VALUE;

        nums = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            nums[i] = Integer.parseInt(st.nextToken());
        }
    }

    private static void sol() throws IOException {
        int left = 0, right = 0;
        int tmp = 0;
        while (right < N) {
            tmp += nums[right];

            while (tmp >= S) {
                ans = Math.min(ans, right - left + 1);
                tmp -= nums[left];
                left++;
            }
            right++;
        }
        bw.write(ans != Integer.MAX_VALUE ? ans + "" : "0");
        bw.flush();
        bw.close();
        br.close();
    }

}
```