```java
import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class BJ_3151_합이_0 {

    private static final BufferedReader  br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter  bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static       StringTokenizer st;

    private static int   N;
    private static long  ans;
    private static int[] students;

    public static void main(String[] args) throws IOException {
        init();
        sol();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());

        students = new int[N];
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            students[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(students);
    }

    private static void sol() throws IOException {
        for (int i = 0; i < N; i++) {
            int left  = i + 1;
            int right = N - 1;

            while (left < right) {
                int leftVal  = students[left];
                int rightVal = students[right];
                int sum      = leftVal + rightVal + students[i];

                if (sum == 0) {
                    if (leftVal == rightVal) {
                        int n = right - left + 1;
                        ans += (long) n * (n - 1) / 2;
                        break;
                    }

                    int cntL = 1;
                    while (leftVal == students[++left]) {
                        cntL++;
                    }

                    int cntR = 1;
                    while (rightVal == students[--right]) {
                        cntR++;
                    }

                    ans += (long) cntL * cntR;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        bw.write(ans + "");
        bw.flush();
        bw.close();
        br.close();
    }

}

```