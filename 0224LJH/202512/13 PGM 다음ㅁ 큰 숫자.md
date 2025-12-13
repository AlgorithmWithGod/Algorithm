```java
import java.io.*;
import java.util.*;

class Solution {
    public int solution(int n) {
        
        int goalCnt = getTwoCnt(n);
    
        int num = n+1;
        
        while (true){
            int target = num;
            int tempTwoCnt = getTwoCnt(target);
            if (tempTwoCnt == goalCnt) {
                break;
            }
            num++;
        }
        return num;
    }
    
    public int getTwoCnt(int n){
        int result = 0;
        while (n > 0){
            if (n%2 != 0) result++;
            n /=2;
        }
        
        return result;
    }
}
```
