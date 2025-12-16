```java
import java.util.*;
class Solution {
    static Map<Integer,Integer> count = new HashMap<>();
    public int solution(int k, int[] tangerine) {
        int answer = 0;
        for(int t : tangerine){
            count.put(t,count.getOrDefault(t,0) + 1);
        }
        List<Integer> countList = new ArrayList<>(count.values());
        countList.sort(Comparator.reverseOrder());
        int sum = 0;
        for(int cur : countList){
            sum+=cur;
            answer++;
            if(sum >= k){
                return answer;
            }
        }
        return answer;
    }
}
```
