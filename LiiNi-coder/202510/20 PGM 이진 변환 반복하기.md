```java
import java.util.*;

class Solution {
    public int[] solution(String s) {
        int[] answer = new int[]{0, 0};
        
        while(!"1".equals(s)){
            // 1개수 확인
            int oneCount = 0;
            for(int i = 0; i<s.length(); i++){
                if(s.charAt(i) == '1')
                    oneCount++;
            }
            answer[1] += s.length() - oneCount;
            // 이진수 s에 대입
            StringBuilder sb = new StringBuilder();
            while(oneCount>1){
                sb.append(Integer.toString(oneCount % 2));
                oneCount /= 2;
            }
            sb.append(Integer.toString(oneCount));
            sb.reverse();
            s = sb.toString();
            answer[0]++;
        }
        
        return answer;
    }
}
```
