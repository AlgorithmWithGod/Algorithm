```java
import java.util.*;

class Solution {
    public int solution(int[] order) {
        int answer = 0;
        Queue<Integer> main = new LinkedList<>();
        for(int i = 1; i <= order.length; i++)
            main.offer(i);
        
        Deque<Integer> sub = new ArrayDeque<>();
        int index = 0;

        for(int target : order){
            while(true){
                if(!main.isEmpty() && main.peek() <= target){
                    if(main.peek() == target){
                        main.poll();
                        answer++;
                        
                        break;
                    } else {
                        sub.offer(main.poll());
                    }
                } else {
                    if(!sub.isEmpty() && sub.peek() == target){
                        sub.poll();
                        answer++;
                    }
                    
                    
                    else {
                        return answer;
                    }
                    break;
                }
            }
        }
        return answer;
    }
}

```
