```java
import java.util.*;
class Solution {
    public int[] solution(int n, String[] words) {
        
        Map<String,Boolean> history = new HashMap<>();
        
        int fail = 0;
        String prev = words[0];
        history.put(prev,true);
        for(int i=1;i<words.length;i++){
            if(prev.charAt(prev.length()-1) == words[i].charAt(0)
               && history.get(words[i]) == null
               && words.length>1){
                prev = words[i];
                history.put(words[i],true);
            }else{
                fail = i;
                break;
            }
        }
        if(fail == 0){
            return new int[]{0,0};
        }
        return new int[]{(fail%n)+1,(fail/n)+1};
    }
}
```
