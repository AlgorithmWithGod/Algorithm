```java
import java.util.*;

class Solution {

    public int solution(String s) {
        int n = s.length();
        int answer = 0;

        for (int i = 0; i < n; i++) {
            if (valid(s, i) == true) {
                answer++;
            }
        }

        return answer;
    }

    private boolean valid(String s, int start) {
        int n = s.length();
        Deque<Character> stack = new ArrayDeque<>();

        for (int k = 0; k < n; k++) {
            char c = s.charAt((start + k) % n);

            if (c == '(' || c == '[' || c == '{') {
                stack.push(c);
            } else {
                if (stack.isEmpty() == true) {
                    return false;
                }

                char top = stack.pop();
                if (match(top, c) == false) {
                    return false;
                }
            }
        }

        return stack.isEmpty();
    }

    private boolean match(char open, char close) {
        if (open == '(' && close == ')') {
            return true;
        }
        if (open == '[' && close == ']') {
            return true;
        }
        if (open == '{' && close == '}') {
            return true;
        }
        return false;
    }
}

```
