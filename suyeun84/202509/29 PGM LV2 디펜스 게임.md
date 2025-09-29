```java
import java.util.*;
class Solution {
    public int solution(int n, int k, int[] enemy) {
        int answer = enemy.length;
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        for (int i = 0; i < enemy.length; i++) {
            pq.offer(enemy[i]);

            if(pq.size() > k) n -= pq.poll();
            
            if (n < 0) return i;
        }
        return answer;
    }
}
```
