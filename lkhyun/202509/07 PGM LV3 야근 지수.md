```java
import java.util.*;
class Solution {
    static PriorityQueue<Integer> pq = new PriorityQueue<>((a,b) -> Integer.compare(b,a));
    public long solution(int n, int[] works) {
        long answer = 0;
        for(int i : works){
            pq.offer(i);
        }
        for(int i=0;i<n;i++){
            if(!pq.isEmpty()){
                int cur = pq.poll();
                if(cur > 1){
                    pq.offer(--cur);
                }
            }else{
                return 0;
            }
        }
        for(int i : pq){
            answer += i*i;
        }
        return answer;
    }
}
```
