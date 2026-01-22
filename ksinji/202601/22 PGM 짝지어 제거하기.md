```java
import java.util.*;

class Solution {
    public int solution(String s) {
        char[] arr = s.toCharArray();
        char[] stack = new char[arr.length];
        int top = 0;

        for (char c : arr) {
            if (top > 0 && stack[top - 1] == c) {
                top--;
            } else {
                stack[top++] = c;
            }
        }

        return top == 0 ? 1 : 0;
    }
}
```
