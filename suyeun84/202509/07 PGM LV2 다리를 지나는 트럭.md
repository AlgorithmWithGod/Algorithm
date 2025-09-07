```java
import java.util.*;

class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
    	Queue q = new LinkedList();
        
        for(int i=0;i<bridge_length-1;i++){
            q.add(0);
        }
        
        int current_w = truck_weights[0];
        q.add(current_w);
        
        int answer = 1;
        int index = 1;
        
        while(!q.isEmpty()){
            answer++;
            
            int removed = (int) q.poll();
            current_w -= removed;

            if(index < truck_weights.length){
                if(current_w + truck_weights[index] <= weight){
                    current_w += truck_weights[index];
                    q.add(truck_weights[index]);
                    index++;
                }else{
                    q.add(0);
                }
            }
        }
        return answer;
    }
}
```
