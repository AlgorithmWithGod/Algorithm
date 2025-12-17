```java
import java.io.*;
import java.util.*;

class Solution {
    public int[] solution(int brown, int yellow) {
        int len = brown+4;
        int half = len/2;
        int ans1 = -1;
        int ans2 = -1;
        int[] answer = new int[2];
        
        for (int width = half-3; width >= 3 ; width--){
            int height = half-width;
            int temp = 0;
            if ((width-2)*(height-2) == yellow){
                answer[0] = width;
                answer[1] = height;
                return answer;
            }
        }
        
        
        
        return answer;
    }
}
```
