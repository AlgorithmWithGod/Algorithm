```java
import java.util.*;

class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        int answer = 0;
        
        Queue<Integer> bridge = new ArrayDeque<>();
        for (int i = 0; i < bridge_length; i++) {
            bridge.add(0);
        }   
        
        int idx = 0;
        int sum = 0;
        
        while(idx < truck_weights.length){
            answer++;
            sum -= bridge.poll();
            
            if (sum+truck_weights[idx] > weight){
                bridge.add(0);
                continue;
            }
            
            bridge.add(truck_weights[idx]);
            sum += truck_weights[idx++];
        }
        return answer+bridge_length;
    }
}
```
