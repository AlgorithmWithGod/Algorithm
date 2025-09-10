```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.StringTokenizer;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        int[] arr = new int[N];
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(br.readLine());
        }

        Arrays.sort(arr);
        int left = 0;
        int right = 0;
        int answer = Integer.MAX_VALUE;
        while (right < N) {
            int diff = arr[right] - arr[left];
            if (left >= right || diff < M) {
                right++;
            } else {
                answer = Math.min(answer, diff);
                left++;
            }
        }
        System.out.println(answer);
    }
}
```
