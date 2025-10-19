```java
import java.util.*;

class Solution {
    public String solution(String s) {
        StringBuilder answer = new StringBuilder();
        boolean isStartOfWord = true;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if (c == ' ') {
                answer.append(c);
                isStartOfWord = true;
            } else {
                if (isStartOfWord) {
                    answer.append(Character.toUpperCase(c));
                } else {
                    answer.append(Character.toLowerCase(c));
                }
                isStartOfWord = false;
            }
        }
        return answer.toString(); 
    }
}

```
