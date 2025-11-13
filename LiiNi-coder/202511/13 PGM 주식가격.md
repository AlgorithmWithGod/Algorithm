```java
import java.util.*;

class Solution {
    public int[] solution(int[] prices) {
        int n = prices.length;
        int[] answer = new int[n];
        ArrayDeque<Integer> stack = new ArrayDeque<>();

        for(int i= 0; i < n; i++){
            while(!stack.isEmpty()){
                if(prices[stack.peekLast()] > prices[i]){
                    int index = stack.pollLast();
                    answer[index] = i - index;
                }else{
                    break;
                }
            }
            stack.offerLast(i);
        }

        
        while(!stack.isEmpty()){
            int idx = stack.pollLast();
            answer[idx] = n - 1 - idx;
        }
        return answer;
    }
}

```
