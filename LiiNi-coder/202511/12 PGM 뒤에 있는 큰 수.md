```java
import java.util.*;

class Solution {
    public int[] solution(int[] numbers) {
        int n = numbers.length;
        int[] answer = new int[n];
        
        Arrays.fill(answer, -1);
        
        Deque<Integer> stack = new ArrayDeque<Integer>();

        for(int i = 0; i< n; i++){
            while(!stack.isEmpty()){
                if(numbers[stack.peek()] < numbers[i]){
                    int index = stack.pop();
                    answer[index] = numbers[i];
                }else{
                    break;
                }
            }
            //
            stack.push(i);
        }

        return answer;
    }
}

```
