```java
import java.util.*;
class Solution {
    public int solution(int[] a) {
        int answer = 0;
        int n = a.length;
        if (n == 1) return 1;
        int[] left = new int[n];
        int[] right = new int[n];
        
        left[0] = a[0];
        for (int i = 1; i < n; i++) {
            left[i] = Math.min(left[i - 1], a[i]);
        }

        right[n - 1] = a[n - 1];
        for (int i = n - 2; i >= 0; i--) {
            right[i] = Math.min(right[i + 1], a[i]);
        }
        for (int i = 0; i < n; i++) {
            if (i == 0 || i == n-1) answer++;
            else {
                if (left[i-1] < a[i] && right[i+1] < a[i]) continue;
                answer++;
            }
        }
        return answer;
    }
}
```
