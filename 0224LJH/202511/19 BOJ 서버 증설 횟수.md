```java
import java.io.*;
import java.util.*;

class Solution {
    public int solution(int[] players, int m, int k) {
        int len = players.length;
        int[] minus = new int[len];
        
        int cur = 0;
        int total = 0;
        
        for (int i = 0; i < len; i++){
            cur -= minus[i];
            
            int limit = m*(cur+1);
            
            if (players[i] < limit) continue;
            
            int diff = players[i] - limit;
            
            int plus = diff/m + 1;
            cur += plus;
            total += plus;
            
            if (i+k < len){
                minus[i+k] = plus;
            }
            
        }
        
        int answer = total;
        return answer;
    }
}
```
