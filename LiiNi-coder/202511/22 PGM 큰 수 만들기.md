```java
import java.util.*;

class Solution {
    public String solution(String number, int k) {
        int len = number.length() - k;

        Deque<Character> stack = new ArrayDeque<>();

        for(int i = 0; i < number.length(); i++){
            char c = number.charAt(i);
            
            while(!stack.isEmpty()){
                if(k<=0 || stack.peekLast() >= c)
                    break;
                stack.pollLast();
                k--;
            }
            stack.offerLast(c);
        }

        while(stack.size() > len){
            stack.pollLast();
        }
        StringBuilder sb = new StringBuilder();
        while(!stack.isEmpty()){
            sb.append(stack.pollFirst());
        }
        return sb.toString();
    }
}

```
