```java
import java.util.*;

class Solution {
    public int solution(int k, int[] tangerine) {
        int answer = 0;
        Map<Integer, Integer> countsAtSize = new TreeMap<>();
        for(int t: tangerine){
            countsAtSize.put(t, countsAtSize.getOrDefault(t, 0) + 1);
        }
        List<Integer> ss = new ArrayList<>(countsAtSize.values());
        Collections.sort(ss, Collections.reverseOrder());
        
        for(int s: ss){
            k -= s;
            answer++;
            if(k<=0){
                break;
            }
        }
        return answer;
    }
}
```
