```
import java.io.*;
import java.util.*;

public class Main {
    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] dist;
    private static int N, sum, answer;
    public static void main(String[] args) throws IOException {
        init();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        sum = 0;
        answer = 0;

        dist = new int[N];

        for (int i = 0; i < N; i++) {
            dist[i] = Integer.parseInt(br.readLine());
            sum += dist[i];
        }

        int left = 0;
        int right = 1;
        int val = dist[right-1];

        while (left < N) {
            answer = Math.max(answer, Math.min(val, sum-val));

            if (val < sum - val) {
                val += dist[right % N];
                right++;
            } else {
                val -= dist[left];
                left++;
            }
        }
    }
}
```
