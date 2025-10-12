```java
import java.util.*;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        int[] answer = {};
        List<Integer> answerList = new ArrayList<Integer>();
        int[] remainDays = new int[progresses.length];
        
        for (int i=0; i<progresses.length; i++){
            int remain = 100 - progresses[i];
            
            if (remain%speeds[i] == 0) {
                remainDays[i] = remain/speeds[i];
            } else {
                remainDays[i] = remain/speeds[i] +1;
            }
        }
        
        int cnt = 1;
        int days = remainDays[0];
        for (int i=1; i<progresses.length; i++){
            if (remainDays[i] > days){
                answerList.add(cnt);
                cnt = 0;
                days = remainDays[i];
            }
            cnt++;       
        }
        
        answerList.add(cnt);
        answer = new int[answerList.size()];
        
        for (int i=0; i<answerList.size(); i++){
            answer[i] = answerList.get(i);
        }
        
        return answer;
    }
}
```
