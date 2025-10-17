```
import java.io.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static char[] input;
    private static int[] a;
    private static int total, answer, rCount;

    public static void main(String[] args) throws IOException {
        init();
        answer = twoPointer();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        input = br.readLine().toCharArray();

        rCount = 0;
        for (char c : input) {
            if (c == 'R') rCount++;
        }

        a = new int[rCount];

        int idx = 0;
        int kCount = 0;

        for (int i = 0; i < input.length; i++) {
            if (input[i] == 'K') {
                total++;
                kCount++;
            } else {
                a[idx++] = kCount;
            }
        }
    }

    private static int twoPointer() {
        if (rCount == 0) return 0;

        int left = 0;
        int right = rCount - 1;
        int max = 0;

        while (left <= right) {
            int leftK = a[left];
            int rightK = total - a[right];

            int k = Math.min(leftK, rightK);
            int r = right - left + 1;

            max = Math.max(max, k * 2 + r);

            if (leftK < rightK) {
                left++;
            } else {
                right--;
            }
        }

        return max;
    }
}
```
