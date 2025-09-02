```java
import java.util.*;
class Solution {
    public int solution(int[] stones, int k) {
        int answer = Integer.MIN_VALUE;
        int start = 0;
        int end = 200000000;
        while (start <= end) {
            int mid = (start + end) / 2;
            int cnt = 0;
            boolean flag = true;
            for (int i = 0; i < stones.length; i++) {
                if (stones[i] - mid < 0) {
                    cnt++;
                } else {
                    cnt = 0;
                }
                if (cnt >= k) {
                    end = mid - 1;
                    flag = false;
                    break;
                }
            }
            if (flag == true) {
                answer = start;
                start = mid + 1;
            }
        }
        return end;
    }
}
```
