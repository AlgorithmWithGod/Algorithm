```java
import java.util.*;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        int n = progresses.length;
        int[] days = new int[n];
        
        for(int i = 0; i < n; i++){
            int remain = 100 - progresses[i];
            if(remain % speeds[i] == 0){
                days[i] = remain / speeds[i] + 0;    
            }else{
                days[i] = remain / speeds[i] + 1;
            }
        }
        List<Integer> result = new ArrayList<>();
        int preDay = days[0];
        int count = 1;
        for(int i = 1; i < n; i++){
            if(days[i] <= preDay){
                count++;
            } else {
                result.add(count);
                preDay = days[i];
                count = 1;
            }
        }
        
        result.add(count);

        int[] answer = new int[result.size()];
        for(int i = 0; i < result.size(); i++){
            answer[i] = result.get(i);
        }
        
        
        
        return answer;
    }
}

```
