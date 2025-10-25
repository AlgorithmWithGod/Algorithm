```java
import java.util.*;

class Solution {
    public int solution(int distance, int[] rocks, int n) {
        Arrays.sort(rocks);
        
        int start = 0;
        int end = distance;
        int answer = 0;
        
        while (start <= end) {
            int mid = (start+end)/2;
            int cnt = cntRemove(rocks, mid, distance);
            if (cnt <= n){
                answer = Math.max(mid, answer);
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        
        return answer;
    }
    
    private int cntRemove(int[] rocks, int mid, int distance){
        int start = 0;
        int cnt = 0;
        
        for (int i=0; i<rocks.length; i++){
            if (rocks[i] - start >= mid) {
                start = rocks[i];
            } else {
                cnt++;
            }
        }
        
        if (distance - start < mid){
            cnt++;
        }    
        return cnt;
    }
}
```
