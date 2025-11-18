```java
import java.util.*;

class Solution {
    public int solution(int[] priorities, int location) {
        PriorityQueue<Integer> pq = new PriorityQueue<>( Collections.reverseOrder());
        for(int p : priorities){
            pq.offer(p);
        }
        int printedCount = 0;
        Deque<int[]> queue = new ArrayDeque<>();
        for(int i = 0; i < priorities.length; i++){
            queue.offerLast(new int[]{ i, priorities[i] });
        }
        
        while(!queue.isEmpty()){
            int[] now = queue.pollFirst();
            int index = now[0];
            int pri = now[1];

            if(pri == pq.peek()){
                pq.poll();
                printedCount++;
                if(index == location){
                    return printedCount;
                }
            }
            
            //다시 큐 보내기
            else {
                queue.offerLast(now);
            }
        }
        return printedCount;
    }
}

```
