```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_2473_세_용액 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int N, selected, left, right;
    private static long sum, min;
    private static int[] solutions, idx;

    public static void main(String[] args) throws IOException {
        init();
        sol();

        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        min = Long.MAX_VALUE;

        idx = new int[3];
        solutions = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            solutions[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(solutions);
    }

    private static void sol() throws IOException {
        for (int i = 0; i < N - 2; i++) {
            selected = solutions[i];

            left = i + 1;
            right = N - 1;
            while (left < right) {
                sum = (long) solutions[left] + solutions[right] + selected;
                System.out.println(selected + " " + solutions[left] + " " + solutions[right]);
                System.out.println(sum + " " + min);

                if (Math.abs(sum) < min) {
                    min = Math.abs(sum);
                    idx[0] = i;
                    idx[1] = left;
                    idx[2] = right;
                }

                if (sum == 0) {
                    bw.write(selected + " " + solutions[left] + " " + solutions[right]);
                    return;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        bw.write(solutions[idx[0]] + " " + solutions[idx[1]] + " " + solutions[idx[2]]);
    }

}
```
