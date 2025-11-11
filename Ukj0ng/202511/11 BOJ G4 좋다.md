```
import java.io.*;
import java.util.*;

public class Main {
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
    private static int[] arr;
    private static int N, answer;
    public static void main(String[] args) throws IOException {
        init();

        if (N == 1) bw.write(1 + "\n");
        else answer = twoPointer();

        bw.write(answer + "\n");
        bw.flush();
        bw.close();
        br.close();
    }

    private static void init() throws IOException {
        N = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());

        arr = new int[N];

        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(arr);
    }

    private static int twoPointer() {
        int result = 0;

        for (int i = 0; i < N; i++) {
            int left = 0;
            int right = N-1;
            while (left < right) {
                if (left == i) left++;
                else if (right == i) right--;
                else if (arr[left]+arr[right] == arr[i]) {
                    result++;
                    break;
                } else if (arr[left]+arr[right] > arr[i]) {
                    right--;
                } else {
                    left++;
                }
            }
        }

        return result;
    }
}
```
