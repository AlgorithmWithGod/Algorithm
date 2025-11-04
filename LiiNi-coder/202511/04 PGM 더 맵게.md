```java
import java.util.*;

class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        Queue<Integer> q = new PriorityQueue<Integer>();
        for(int s: scoville){
            q.offer(s);
        }
        boolean isImpossible = false;
        while(q.peek() < K){
            if(q.size() < 2){
                isImpossible = true;
                break;
            }
            int s1 = q.poll();
            int s2 = q.poll();
            q.offer(s1 + s2*2);
            answer++;
        }
        return (isImpossible)? -1 : answer;
    }
}
```
