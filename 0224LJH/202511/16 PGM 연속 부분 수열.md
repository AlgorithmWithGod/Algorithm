```java
import java.io.*;
import java.util.*;

class Solution {
    
    static HashSet<Integer> set = new HashSet<>();
    
    
    public int solution(int[] elements) {
        int len = elements.length;
        
        for (int i = 1; i <= len; i++){
            int curLen = i;
            
            int curSum = 0;
            for (int j = 0; j < curLen; j++){
                curSum += elements[j];
            }
            
            int st = 0;
            int end = curLen-1;
            set.add(curSum);
            
            for (int j = 1; j < len; j++){
                curSum -= elements[st];
                st++;
                end++;
                end %= len;
                curSum += elements[end];
                
                set.add(curSum);
            }
            
        }
        
        
        int answer = set.size();
        return answer;
    }
}
```
