```java
import java.util.*;

class Solution {
    public int solution(int[][] routes) {
        Arrays.sort(routes, (a, b) -> Integer.compare(a[1], b[1]));
        
        int answer = 0;
        int camera = Integer.MIN_VALUE;
        
        for (int[] r : routes){
            int s = r[0];
            int e = r[1];
            
            if (camera < s){
                camera = e;
                answer++;
            }
        }
        
        return answer;
    }
}
```
