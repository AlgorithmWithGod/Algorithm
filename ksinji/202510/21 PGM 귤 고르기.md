```java
import java.util.*;

class Solution {
    public int solution(int k, int[] tangerine) {
        int answer = 0;
        Map<Integer, Integer> count = new HashMap<>();
        
        for (int i : tangerine){
            count.put(i, count.getOrDefault(i, 0)+1);
        }
        
        List<Integer> countList = new ArrayList<>();
        
        for (int i : count.values()){
            countList.add(i);
        }
        
        Collections.sort(countList, Collections.reverseOrder());
        
        int sum = 0;
        for (int i : countList){
            sum += i;
            answer++;
            if (sum >= k){
                return answer;
            }
        }
        return answer;
    }
}
```
