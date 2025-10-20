```java
import java.io.*;
import java.util.*;

class Solution {
    public String solution(String s) {
        StringTokenizer st = new StringTokenizer(s);
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        while(st.hasMoreTokens()){
            int num = Integer.parseInt(st.nextToken());
            min = Math.min(min,num);
            max = Math.max(max,num);
        }
        StringBuilder sb = new StringBuilder();
        sb.append(min).append(" ").append(max);
        String answer = sb.toString();
        return answer;
    }
}
```
