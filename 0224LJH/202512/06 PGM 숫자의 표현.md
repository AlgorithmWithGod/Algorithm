```java
import java.io.*;
import java.util.*;

class Solution {
    public int solution(int n) {
        int start = 1;
        int end = 1;
        int curSum = 1;
        
        int answer = 0;
        
        while (end <= n){
            if (curSum == n){
                answer++;
                end++;
                curSum += end;
            }else if (curSum < n){
                end++;
                curSum += end;
            }else{
                curSum -= start;
                start++;
            }
        }
        return answer;
    }
}
```
