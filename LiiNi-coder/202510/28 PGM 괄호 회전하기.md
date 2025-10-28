```java
import java.util.*;
class Solution {
    public int solution(String s) {
        char[] cs = s.toCharArray();
        int answer = 0;
        Deque<Character> q = new ArrayDeque<Character>();
        for(int i = 0; i<s.length(); i++){
            q = new ArrayDeque<Character>();
            for(int d = 0; d<s.length(); d++){
                
                int id = (i+d) % s.length();
                char now = cs[id];
                Character pre = q.peekLast();
                if(pre == null){
                    q.offer(now);
                }
                else if(pre == '(' && now == ')'){
                    q.pollLast();
                }else if(pre == '{' && now == '}'){
                    q.pollLast();
                }else if(pre == '[' && now == ']'){
                    q.pollLast();
                }else{
                    q.offer(now);
                }
            }
            if(q.size() ==0)answer++;
        }   
        
        return answer;
    }
}
```
