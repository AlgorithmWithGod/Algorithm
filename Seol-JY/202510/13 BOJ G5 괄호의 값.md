```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String s = br.readLine();
        
        System.out.println(solution(s));
    }
    
    static int solution(String s) {
        Deque<Character> deque = new ArrayDeque<>();
        int result = 0;
        int temp = 1;
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            
            if (c == '(') {
                deque.push(c);
                temp *= 2;
            } 
            else if (c == '[') {
                deque.push(c);
                temp *= 3;
            } 
            else if (c == ')') {
                if (deque.isEmpty() || deque.peek() != '(') {
                    return 0;
                }
                
                if (s.charAt(i - 1) == '(') {
                    result += temp;
                }
                
                deque.pop();
                temp /= 2;
            } 
            else if (c == ']') {
                if (deque.isEmpty() || deque.peek() != '[') {
                    return 0;
                }
                
                if (s.charAt(i - 1) == '[') {
                    result += temp;
                }
                
                deque.pop();
                temp /= 3;
            }
        }
        
        return deque.isEmpty() ? result : 0;
    }
}
```
