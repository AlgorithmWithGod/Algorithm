```java
import java.util.*;

class Solution {
    public int solution(String s) {
        int answer = 0;
        for(int i=0;i<s.length();i++){
            Stack<Character> stk = new Stack<>();
            for(int j = i;j<s.length();j++){
                if(s.charAt(j) == ')'){
                    if(stk.isEmpty() || stk.peek() != '('){
                        stk.push(s.charAt(j));
                    }else{
                        stk.pop();
                    }
                }else if(s.charAt(j) == '}'){
                    if(stk.isEmpty() || stk.peek() != '{'){
                        stk.push(s.charAt(j));
                    }else{
                        stk.pop();
                    }
                }else if(s.charAt(j) == ']'){
                    if(stk.isEmpty() || stk.peek() != '['){
                        stk.push(s.charAt(j));
                    }else{
                        stk.pop();
                    }
                }else{
                    stk.push(s.charAt(j));
                }
            }
            for(int j = 0;j<i;j++){
                if(s.charAt(j) == ')'){
                    if(stk.isEmpty() || stk.peek() != '('){
                        stk.push(s.charAt(j));
                    }else{
                        stk.pop();
                    }
                }else if(s.charAt(j) == '}'){
                    if(stk.isEmpty() || stk.peek() != '{'){
                        stk.push(s.charAt(j));
                    }else{
                        stk.pop();
                    }
                }else if(s.charAt(j) == ']'){
                    if(stk.isEmpty() || stk.peek() != '['){
                        stk.push(s.charAt(j));
                    }else{
                        stk.pop();
                    }
                }else{
                    stk.push(s.charAt(j));
                }
            }
            if(stk.size() == 0){
                answer++;
            }
        }
        
        return answer;
    }
}
```
