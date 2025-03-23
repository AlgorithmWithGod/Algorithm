```java
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int k = sc.nextInt();
        // 이분탐색
        long left = 0L;
        long right = (long) n * n;
        long answer = 0;
        while (left <= right) {
            long mid = (left + right) / 2;
            long cnt = 0;
            for (int i = 1; i <= n; i++) {
                cnt += Math.min(mid / i, n);
            }
            if (cnt >= k) {
                answer = mid;
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        System.out.println(answer);
    }
}
```
