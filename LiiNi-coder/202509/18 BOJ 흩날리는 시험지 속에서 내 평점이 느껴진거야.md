```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) throws IOException {
        var br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());
        int[] arr = new int[N];
        
        st = new StringTokenizer(br.readLine());
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        long left = Arrays.stream(arr).min().getAsInt();
        long right = 0;
        for (int x : arr)
            right += x;

        long answer = 0;
        while(left <= right) {
            long mid = (left + right) / 2;
            int groupCount = 0;
            long sum = 0;
            
            for (int i = 0; i < N; i++) {
                sum += arr[i];
                if (sum >= mid) {
                    groupCount++;
                    sum = 0;
                }
            }
            
            if (groupCount >= K) {
                answer = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        System.out.println(answer);
    }
}

```
