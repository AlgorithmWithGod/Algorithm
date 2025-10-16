```java
import java.util.*;

class Solution {
    public int solution(int[] scoville, int K) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        for (int i: scoville){
            pq.add(i);
        }
        
        int answer = 0;
        
        while (!pq.isEmpty() && pq.peek() < K) {
            // pq의 크기가 2 미만이면 음식 섞기 불가
            // 근데 모든 음식의 스코빌 지수가 아직 K 이상이 아니므로 -1 리턴
            if (pq.size() < 2){
                return -1;
            }
            
            int first = pq.poll();
            int second = pq.poll();
            int newS = first + (second*2);
            
            pq.add(newS);
            answer++;
        }
        
        return answer;
    }
}
```