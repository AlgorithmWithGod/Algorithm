```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] weight;
    private static int N, sum, answer;

    public static void main(String[] args) throws IOException {
        init();

        bw.write(answer+"\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        weight = new int[N];

        StringTokenizer st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            weight[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(weight);

        sum = 0;

        for (int i = 0; i < N; i++) {
            if (weight[i] > sum+1) {
                break;
            }
            sum += weight[i];
        }

        answer = sum+1;
    }
}
```
