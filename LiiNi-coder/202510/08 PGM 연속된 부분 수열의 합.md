```java
import java.util.*;

class Solution {
    public int[] solution(int[] sequence, int k) {
        int[] answer = {-1, -1};
        int l = 0, r = 0, sum = 0;
        Deque<Integer> q = new ArrayDeque<>();
        while(r <= sequence.length){
            if(sum == k){
                if(answer[0] == -1 || (r - l - 1) < (answer[1] - answer[0])){
                    answer[0] = l;
                    answer[1] = r -1;
                }
            }
            
            
            if(sum >= k){
                sum -= q.poll();
                l++;
            }else{
                if(r == sequence.length)
                    break;
                sum += sequence[r];
                q.add(sequence[r]);
                r++;
            }
        }
        return answer;
    }
}

```
