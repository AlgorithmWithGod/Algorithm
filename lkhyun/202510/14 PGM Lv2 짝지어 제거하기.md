```java
import java.util.*;
class Solution
{
    public int solution(String s)
    {
        int answer = -1;
        Stack<Character> stk = new Stack<>();
        
        for(char c : s.toCharArray()){
            if(stk.isEmpty() || stk.peek() != c){
                stk.push(c);
            }else{
                stk.pop();
            }
        }
        
        return stk.isEmpty() ? 1 : 0;
    }
}
```
