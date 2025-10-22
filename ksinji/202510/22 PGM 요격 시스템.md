```java
import java.util.*;

class Solution {
    public int solution(int[][] targets) {
        Arrays.sort(targets, (a, b) -> Integer.compare(a[1], b[1]));

        int answer = 0;
        int lastEnd = Integer.MIN_VALUE;

        for (int[] t : targets) {
            int s = t[0], e = t[1];
            if (s >= lastEnd) {
                answer++;
                lastEnd = e;
            }
        }
        return answer;
    }
}
```
