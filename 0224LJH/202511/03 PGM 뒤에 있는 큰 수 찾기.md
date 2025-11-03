```java
import java.io.*;
import java.util.*;

class Solution {
    public int[] solution(int[] numbers) {
        int n = numbers.length;
        int[] answer = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = n - 1; i >= 0; i--) {
            // 현재 원소보다 작거나 같은 스택의 원소들을 제거
            while (!stack.isEmpty() && stack.peek() <= numbers[i]) {
                stack.pop();
            }
            
            if (stack.isEmpty()) {
                answer[i] = -1;
            } else {
                // 스택의 맨 위가 뒷 큰수
                answer[i] = stack.peek();
            }

            stack.push(numbers[i]);
        }
        
        return answer;
    }
}
```
